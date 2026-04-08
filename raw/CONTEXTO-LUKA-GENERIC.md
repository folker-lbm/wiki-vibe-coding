# Contexto: Luka — Agentic Coding Setup
**Versión:** 2.0 — Abril 2026

---

## Quién soy
Luka Bureo. No soy programador. Empecé a usar la terminal, Git y Claude Code
desde cero recientemente. Aprendo rápido pero necesito explicaciones sin asumir
conocimiento técnico. Uso agentic coding para construir productos digitales
sin depender de programadores.

---

## Mi setup

### Hardware y suscripciones
- Mac Mini (Apple Silicon)
- Claude Max 5x (100€/mes)
- Google AI Pro (Gemini)
- Antigravity IDE (fork de VS Code con IA)

### Herramientas instaladas
- Homebrew, Node.js, Git, GitHub CLI (`gh`), Bun, NVM
- Claude Code (terminal + Antigravity)
- Gemini CLI, Codex CLI
- tmux (opcional, para ver agentes en paralelo)
- Obsidian (visor de wikis personales)
- Obsidian Web Clipper (extensión Chrome para clipear artículos a raw/)

### Configuración de Claude Code (~/.claude/settings.json)
```json
{
  "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" },
  "permissions": {
    "allow": ["Bash(*)", "Read(*)", "Write(*)", "Edit(*)", "WebFetch(*)", "mcp__*"]
  }
}
```

### Skills instalados (~/.claude/skills/)
**Desarrollo:**
- react-best-practices, composition-patterns, web-design-guidelines (Vercel)
- deploy-to-vercel (Vercel)

**Diseño:**
- frontend-design (Anthropic oficial)
- bencium-innovative-ux-designer
- creative-director (20+ metodologías de diseño)

**Wiki / Second Brain:**
- second-brain (NicholasSpisak) — incluye 4 comandos:
  - /second-brain — scaffolding de nueva wiki
  - /second-brain-ingest — ingesta de fuentes
  - /second-brain-query — consultas contra la wiki
  - /second-brain-lint — health check mensual

**Otros:**
- humanizer (eliminar tono IA de textos)
- last30days (research en Reddit, X, YouTube, HN)

### Plugins
- Superpowers (obra) — TDD, systematic-debugging, subagent-driven-development
- code-simplifier (Anthropic)
- Telegram channel (notificaciones al móvil)

---

## Mi equipo de agentes (6 agentes)

Guardados en `~/Desktop/Vibe Coding/Agentes/`. Se copian a cada proyecto nuevo.

| Agente | Modelo | Rol |
|--------|--------|-----|
| @architect | **Opus** | Team lead. Coordina. NUNCA ejecuta. |
| @designer | **Opus** | Research + UX + UI + HTML previews |
| @design-evaluator | **Opus** | Puntúa diseño con 4 criterios. Loop GAN. |
| @developer | **Sonnet** | Full-stack. Implementa y despliega. |
| @reviewer | **Opus** | Code review + devil's advocate |
| @qa-tester | **Sonnet** | Prueba la app como usuario real |

### El loop evaluador (GAN)
El @designer genera, el @design-evaluator puntúa. Si <8.5, vuelve al designer.
Máximo 5 rondas. Basado en el artículo de Anthropic sobre harness design.

**4 criterios (pesos correctos):**
| Criterio | Peso |
|----------|------|
| Design Quality | 30% |
| Originality | 25% |
| Craft | 15% |
| Functionality | 30% |

**Threshold: 8.5/10** — el diseño debe ser destacable, no solo correcto.
- <6.0: FAIL — replanteamiento total
- 6.0-8.4: ITERATE — vuelve al designer con feedback
- ≥8.5: PASS — listo para aprobación del usuario

### 3 slash commands
Guardados en `~/Desktop/Vibe Coding/commands/`.
- `/delegate` — forzar al architect a delegar en vez de hacer él
- `/evaluate-design` — forzar ronda de evaluación de diseño
- `/reset` — context reset estructurado (escribe estado, compacta, relee todo)

---

## Estructura de carpetas

### Reutilizables (escritorio)
```
~/Desktop/Vibe Coding/
├── Agentes/           ← 6 .md maestros (mayúscula, español)
├── commands/          ← 3 slash commands
├── design-systems/    ← Un design system por marca/proyecto
├── workflows/         ← Documentos de proceso
├── prompts/           ← Prompts reutilizables
└── archivo-obsoleto/  ← Versiones antiguas archivadas
```

### Global (una vez por ordenador)
```
~/.claude/
├── settings.json      ← Permisos, Agent Teams
├── skills/            ← Skills globales
├── plugins/           ← Superpowers, code-simplifier
└── channels/telegram/ ← Token del bot
```

### Por proyecto
```
~/proyecto/
├── .claude/
│   ├── agents/        ← 6 agentes (copiados de Vibe Coding/Agentes/)
│   └── commands/      ← 3 comandos (copiados de Vibe Coding/commands/)
├── CLAUDE.md          ← Contexto del proyecto (corto, ~1K tokens)
├── DESIGN-SYSTEM.md   ← Identidad visual del proyecto
├── GEMINI.md          ← Copia de CLAUDE.md
├── misc/
│   ├── strategy/
│   ├── design/
│   │   ├── ux/
│   │   ├── ui/
│   │   ├── previews/
│   │   └── references/
│   ├── review/
│   └── coding-team/
└── src/               ← Código
```

---

## Mis wikis personales (segundo cerebro)

Sistema basado en el patrón LLM Wiki de Andrej Karpathy (abril 2026).
Cada wiki es un repo público en GitHub con esta estructura:
```
wiki-nombre/
├── CLAUDE.md          ← Instrucciones del agente mantenedor
├── raw/               ← Fuentes originales (NUNCA modificar)
│   └── assets/
└── wiki/              ← Conocimiento compilado (el LLM escribe esto)
    ├── areas/
    ├── ideas/
    ├── referencias/
    ├── workflows/
    ├── diario/        ← Solo en wiki-personal
    ├── index.md
    └── log.md
```

### Wikis activas
| Wiki | GitHub | Contenido |
|------|--------|-----------|
| wiki-vibe-coding | github.com/folker-lbm/wiki-vibe-coding | Agentic coding, Claude Code, agentes, workflows |
| wiki-personal | github.com/folker-lbm/wiki-personal | Diario, ideas, filosofía, economía, trading |

### Loop diario de la wiki
1. Encuentras algo interesante → Web Clipper → raw/
2. `wiki` (alias en terminal) → `/second-brain-ingest`
3. Para consultar: pregunta en lenguaje natural
4. Mensual: `/second-brain-lint`

### Alias de terminal
```bash
alias wiki="cd ~/wiki-vibe-coding && claude"
```

---

## Proyecto activo: Wiki Brain

App web personal desplegada en Vercel para acceder a las wikis sin terminal.
- Repo local: `~/wiki-chat`
- Stack: Next.js 14, Tailwind, API Anthropic
- Design system: Linear.app
- Funciones: chat con wiki, panel lateral navegable, grafo de conceptos,
  flashcards con repaso espaciado, resumen diario, sugerencias

---

## Workflow: proyecto nuevo

```bash
# 1. Crear y estructurar
mkdir ~/proyecto && cd ~/proyecto
mkdir -p .claude/agents .claude/commands misc/strategy misc/design/ux \
  misc/design/ui misc/design/previews misc/design/references misc/review

# 2. Copiar agentes y comandos
cp ~/Desktop/Vibe\ Coding/Agentes/*.md .claude/agents/
cp ~/Desktop/Vibe\ Coding/commands/*.md .claude/commands/

# 3. Crear CLAUDE.md
# 4. Crear o copiar DESIGN-SYSTEM.md
# 5. cp CLAUDE.md GEMINI.md
# 6. Copiar archivos de referencia

# 7. Git + GitHub
git init && git add -A && git commit -m "setup inicial"
gh repo create nombre --private --source=. --push

# 8. Arrancar (SIEMPRE con estos flags)
claude --dangerously-skip-permissions --channels plugin:telegram@claude-plugins-official
```

---

## Workflow: modo nocturno

```bash
caffeinate -s &
```
Prompt:
```
Modo autónomo nocturno. No esperes aprobación. Trabaja seguido.
Spawna @reviewer y @qa-tester. Corrige via @developer. Commit todo.
Prepara deploy pero NO despliegues. Avísame por Telegram.
```

---

## Problemas conocidos y soluciones

### El architect no delega
Solución: `/delegate`, `/reset` cada hora.

### Diseño mediocre / genérico
Solución: loop GAN con threshold 8.5, DESIGN-SYSTEM.md con alma, referencias visuales.

### Context rot
Solución: `/reset` periódico.

### Wiki con información incorrecta
Causa: el lint detecta errores estructurales pero no de contenido.
Solución: corregir en raw/ y re-ingestar.

### Telegram se desconecta
Reiniciar con `--channels`.

### Mac se duerme
`caffeinate -s &` antes de dejarlo solo.

---

## Principios que he aprendido

### Sobre diseño
- Mockups antes que código. Siempre.
- Threshold 8.5 — el diseño debe ser destacable, no solo correcto.
- DESIGN-SYSTEM.md necesita alma, no solo tokens de color.

### Sobre el segundo cerebro
- Una wiki por dominio.
- Web Clipper es el hábito clave — un clic cuando lees algo.
- Lint mensual obligatorio.
- Corregir siempre en raw/, nunca en la wiki directamente.

### Sobre agentes
- 6 agentes es el sweet spot.
- 4 Opus + 2 Sonnet.
- El architect tiende a hacer cosas él mismo — vigilar siempre.

### Sobre context engineering
- /reset cada hora o entre fases.
- Skills = contexto bajo demanda.
- CLAUDE.md corto (~1K tokens).

### Sobre el proceso
- Describe problemas, no soluciones.
- "Aprobado" es la única señal para avanzar.
- Commits frecuentes antes de cada fase.
- Si algo se hace dos veces, convertirlo en skill o command.

---

## Cómo prefiero que me hables
- En español
- Sin asumir conocimiento técnico
- Directo y práctico — dame los comandos, no solo la teoría
- Si algo puede salir mal, avísame antes
- Cuando me des código, dime exactamente dónde ejecutarlo
