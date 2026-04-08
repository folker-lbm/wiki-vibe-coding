---
tags: [claude-code, features, channels, batch, hooks, agent-teams, loop]
sources: ["10 hidden Claude code features that 99.9% ignore.md", "The Claude Features Nobody Talks About (But Everyone Is Paying For).md"]
created: 2026-04-08
updated: 2026-04-08
---

# Claude Code — Features Avanzadas

Features documentadas pero que la mayoría de usuarios desconoce. Extraídas de la documentación oficial (hooks reference, channels page, experimental flags).

## Channels

```bash
claude --channels plugin:telegram@claude-plugins-official
```

Claude accesible vía Telegram, Discord, o iMessage **dentro de una sesión activa**. No es polling ni webhook a nueva sesión — el evento llega al session que ya tiene contexto completo.

**Caso de uso**: CI falla a las 2am, Claude recibe el evento, diagnostica, y te envía un resumen por Telegram. Respondes "do it" y aplica el fix.

## /batch — Agentes Paralelos

```
/batch migrate src/ from Solid to React
```

Claude divide el codebase en unidades independientes, pide aprobación, y lanza un agente por unidad en **git worktree aislado**. Cada agente implementa, corre tests, y abre un PR. Resultado: stack de PRs, no un diff de 4000 líneas.

Rango: 5-30 agentes paralelos. Skill bundled (disponible en toda sesión).

## Agent Teams

```bash
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

A diferencia de sub-agents (que solo reportan al usuario), los teammates **comparten task list y se envían mensajes entre sí**. Uno encuentra un security issue → lo comunica al teammate de arquitectura → el architect revisa el plan → el devil's advocate pushes back.

Se puede requerir que cada teammate presente plan para aprobación antes de escribir código.

## /init mejorado

```bash
CLAUDE_CODE_NEW_INIT=1
```

Setup multi-paso: escanea codebase, identifica build commands/tests/arquitectura, pregunta gaps, muestra propuesta para review. Produce un CLAUDE.md tailored al proyecto real.

## Hooks Avanzados

### TaskCompleted (veto)
```
TaskCompleted → tu script → exit 2 para bloquear
```
Exit code 2 = tu mensaje vuelve a Claude: "tests still failing, task is not done." Claude sigue trabajando. Quality enforcement baked into the agent loop.

### TaskCreated
Rechazar tareas que no cumplan estándares antes de que empiecen.

### CwdChanged (auto-env)
```
CwdChanged → trigger direnv reload
```
En monorepo: Claude entra a `packages/payments` → env vars de ese package se cargan automáticamente. Cambia a `packages/auth` → otras vars, auto-reload.

### FileChanged (reactivo)
```
FileChanged (matcher: "package-lock.json") → run security audit
```
Matcher define qué archivos vigilar. Convierte a Claude de algo que prompteas a algo que **vigila tu proyecto y reacciona**.

## /loop + Skills

```
/loop 20m /simplify focus on the auth module
```

El prompt programado puede ser otra invocación de skill. PR review, security checker, documentation linter — cualquier skill en un timer mientras trabajas en otra cosa.

## Subagent Persistent Memory

```
memory: user → ~/.claude/agent-memory/
```

Al crear un custom subagent, se habilita directorio de memoria persistente. El subagent escribe lo que aprende a disco y lo carga al inicio de cada sesión futura. Code reviewer que recuerda tus errores recurrentes de async.

## HTML Comments en CLAUDE.md

```html
<!-- Last reviewed: March 2025. Update auth section after OAuth migration. -->
```

Comentarios HTML block se stripean antes de inyectar al contexto. Notas para humanos que no gastan tokens. Documentado en una sola frase en la página de memory.

## Features de Claude (no solo Claude Code)

De [Source: claude-features-nobody-talks-about.md]:

| Feature | Para qué |
|---------|----------|
| **Projects** | Workspaces persistentes con memoria y documentos |
| **Deep Research** | 3-10 min de investigación multi-fuente con citas |
| **Artifacts** | Ficheros interactivos: dashboards, React, SVG, presentations |
| **Memory** | Recuerda preferencias across conversations |
| **Styles** | Presets de tono (Work, Writing, Technical, Quick) |
| **Code Execution** | Ejecuta Python/JS en el chat |
| **File Creation** | Genera Word, Excel, PPT, PDF descargables |
| **[[Claude Cowork]]** | Background tasks con computer use + Dispatch |

Ver también: [[claude-code-arquitectura]], [[agentes]], [[optimizacion-tokens]], [[setup]]
