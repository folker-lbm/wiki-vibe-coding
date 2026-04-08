---
tags: [claude-code, arquitectura, harness, infrastructure, agent-loop]
sources: ["How I built harness for my agent using Claude Code leaks.md"]
created: 2026-04-08
updated: 2026-04-08
---

# Arquitectura de Claude Code

Análisis de la arquitectura interna de Claude Code basado en su código fuente abierto (55 dirs, 331 módulos TypeScript).

## Las 4 capas (no 3)

La industria habla de 3 capas (Weights → Context → Harness). Claude Code demuestra que hay una cuarta:

| Capa | Qué es | Ejemplo en Claude Code |
|------|--------|----------------------|
| 1. Model Weights | Inteligencia congelada | Claude API |
| 2. Context | Input en runtime | Prompts, historial, docs |
| 3. Harness | Entorno diseñado del agente | Tools, loops, error handling |
| 4. **Infrastructure** | Multi-tenancy, RBAC, aislamiento, persistencia, coordinación | CLAUDE.md hierarchy, task list, worktrees, permisos |

> SWE-agent (Princeton NLP) demostró 64% de mejora cambiando solo capas 2-3, sin tocar el modelo. [Source: claude-code-harness-architecture.md]

## Agent Loop — Async Generator

El corazón vive en `query.ts` (1,729 líneas). Es un `async function*` (generator), no un while loop.

**Ventajas sobre while loop:**
- **Streaming**: yield de eventos conforme llegan tokens
- **Cancelación**: el caller deja de llamar `.next()`, cleanup en `finally`
- **Composabilidad**: REPL, sub-agents y tests consumen la misma función
- **Backpressure**: si el consumer no tira, la producción pausa

**5 fases por iteración:**
1. **Setup** — budgets, compactación si necesario, validar tokens
2. **Model Invocation** — streaming + ejecución de tools en paralelo durante el stream
3. **Error Recovery & Compaction** — prompt-too-long→compactar, max_output→escalar, overflow→compactar media
4. **Tool Execution** — tools pendientes + summaries via Haiku
5. **Continuation Decision** — stop_reason, maxTurns, hooks, abort signals

## Tool Execution

### Concurrency Classification

Cada tool se clasifica al definirlo:

| Tipo | Ejecución | Ejemplo |
|------|-----------|---------|
| Read-only | Paralelo (hasta 10) | Glob, Grep, Read, WebFetch |
| Write/mutate | Serial | Bash (mutaciones), Edit, Write |

Resultado: 2-5x speedup sin race conditions.

### Streaming Tool Executor

Ejecuta tools **durante** el streaming, antes de que el modelo termine de generar. Un Grep empieza a correr en cuanto su input JSON está completo en el stream. Ahorra 2-5 segundos por turno multi-tool.

- Si un tool en batch falla, `siblingAbortController` mata siblings pero no el parent
- Resultados se yieldan en orden original aunque tool 2 termine antes que tool 1
- Si streaming falla, fallback a non-streaming con synthetic error results

### Tool Result Budgeting

- Cada tool especifica `maxResultSizeChars`
- Resultados grandes se persisten a disco → modelo recibe file path + preview
- `applyToolResultBudget()` limita total de tokens de tool results antes de cada API call

## Context Compaction

4 estrategias ordenadas de barata a cara:

1. **Microcompact** — cada turno. Si un tool result no cambió desde la última llamada, reemplaza con referencia cacheada. Coste: ~0
2. **Snip Compact** — cerca del límite. Corta mensajes del inicio preservando "protected tail" reciente. Sin model call
3. **Auto Compact** — cuando snip no basta. Model call separado para summarizar. Tracks compaction state para evitar loops
4. **Context Collapse** — sessions largas, feature flag. Compresión multi-fase: tool results → thinking blocks → secciones enteras

> La jerarquía importa: paga compactación cara solo cuando la barata falla. [Source: claude-code-harness-architecture.md]

## Prompt Cache Design

System prompt dividido en dos zonas por `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`:

- **Above** (~80%): idéntico para todos los usuarios/sessions → cache hit global
- **Below**: memoized (una vez por session) o volatile (cada turno, minimizado)

Contexto de usuario (git status, CLAUDE.md) inyectado como **primer user message** en `<system-reminder>`, no en system prompt → no rompe el cache.

> Diseñar el prompt para cache efficiency es una de las decisiones de mayor leverage en producción. Diferencia entre $0.02 y $0.20 por sesión. [Source: claude-code-harness-architecture.md]

## Permission System — 7 Stages

Pipeline de 7 etapas con deny rules que cascadan de enterprise a session. Reglas con glob-like matching sobre tool name + input.

**Modos progresivos de confianza:**
- `default` → aprueba cada acción
- `acceptEdits` → auto-aprueba ediciones
- `bypassPermissions` → todo auto-aprobado

Hooks como escape hatch: scripts que reciben detalles del tool call y retornan `{"decision": "approve"|"block"}`.

## Error Recovery — 823 líneas

`services/api/withRetry.ts` — cada clase de error tiene recovery específico:

| Error | Recovery |
|-------|----------|
| 429 (rate limit) | Retry-After <20s→retry, >20s→30min cooldown, overage→disable fast mode |
| 529 (overloaded) | 3 consecutivos + fallback model→switch. Background→bail |
| 400 (context overflow) | Parse tokens, recalcular budget, retry con ajuste |
| 401/403 (auth) | Clear cache, refresh OAuth, retry |
| Network (ECONNRESET, timeout) | Disable keep-alive, retry nueva conexión |

Backoff: `min(500ms × 2^attempt, 32s) + random jitter`

## Sub-Agent Architecture

- Cada sub-agent tiene contexto aislado, tools propios, working directory propio
- `appState` es no-op setter para hijos — no pueden mutar estado del parent
- File state caches clonados para evitar contaminación

### Git Worktree Isolation
- Un agente, un worktree (`git worktree add`, branch `worktree-<slug>`)
- Symlink de `node_modules` y `.cache` para no duplicar
- Copia CLAUDE.md, settings, .env al worktree

### 3 Backends de ejecución
1. **In-process** — más rápido, shared memory
2. **Tmux pane** — aislamiento visual, cada agente en su tab
3. **Remote (CCR)** — aislamiento completo de máquina

### Coordinación
Task list en disco: `~/.claude/tasks/<taskListId>/<taskId>.json`. File-based locking con exponential backoff (30 retries, 5-100ms). High water mark para evitar reuso de IDs.

## Extensibility — 4 mecanismos sin modificar código

1. **Skills** — markdown + YAML frontmatter. 5 fuentes: bundled, project, user, plugin, MCP. Path-based discovery
2. **Hooks** — 6 tipos (shell, LLM eval, agentic, HTTP, TypeScript, in-memory). Fires on PreToolUse, PostToolUse, SessionStart, FileChanged, Stop
3. **MCP** — 5 transportes (stdio, SSE, HTTP streaming, WebSocket, in-process). 3 niveles de config
4. **Plugins** — directorios con skills, agents, hooks, config

> Principio: composición sobre modificación. Extender añadiendo, no cambiando. [Source: claude-code-harness-architecture.md]

Ver también: [[agentes]], [[principios]], [[claude-code-features-avanzadas]]
