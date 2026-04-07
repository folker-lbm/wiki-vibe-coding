# Contexto: Luka — Agentic Coding Setup

## Quién soy
Luka Bureo. No soy programador. Empecé a usar la terminal, Git y Claude Code 
desde cero recientemente. Aprendo rápido pero necesito explicaciones sin asumir 
conocimiento técnico. Uso agentic coding para construir productos digitales 
sin depender de programadores.

## Mi setup

### Hardware y suscripciones
- Mac Mini (Apple Silicon)
- Claude Max 5x (100€/mes)
- Google AI Pro (Gemini)
- Antigravity IDE (fork de VS Code con IA)

### Herramientas instaladas
- Homebrew, Node.js, Git, GitHub CLI (`gh`), Bun
- Claude Code (terminal + Antigravity)
- Gemini CLI, Codex CLI (disponibles para orquestar en el futuro)
- tmux (opcional, para ver agentes en paralelo)

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

**Otros:**
- humanizer (eliminar tono IA de textos)
- last30days (research en Reddit, X, YouTube, HN)

**Por proyecto (no global):**
- ui-ux-pro-max (instalar con `uipro init --ai claude`)

### Plugins
- Superpowers (obra) — TDD, systematic-debugging, subagent-driven-development
- code-simplifier (Anthropic)
- Telegram channel (notificaciones al móvil)

## Mi equipo de agentes (6 agentes)

Guardados en `~/Desktop/Vibe Coding/Agentes/`. Se copian a cada proyecto nuevo.

| Agente | Modelo | Rol |
|--------|--------|-----|
| @architect | Sonnet | Team lead. Coordina. NUNCA ejecuta. |
| @designer | Opus | Research + UX + UI + HTML previews |
| @design-evaluator | Opus | Puntúa diseño con 4 criterios. Loop GAN. |
| @developer | Sonnet | Full-stack. Implementa y despliega. |
| @reviewer | Sonnet | Code review + devil's advocate |
| @qa-tester | Sonnet | Prueba la app como usuario real |

### El loop evaluador (GAN)
El @designer genera, el @design-evaluator puntúa. Si <7.0, vuelve al designer.
Máximo 5 rondas. Basado en el artículo de Anthropic sobre harness design.

**4 criterios:**
- Design Quality (30%) — coherencia visual, identidad
- Originality (25%) — decisiones creativas vs template
- Craft (15%) — tipografía, spacing, color, responsive
- Functionality & Architecture (30%) — usabilidad, flujos, jerarquía, escalabilidad

### 3 slash commands
Guardados en `~/Desktop/Vibe Coding/commands/`.
- `/delegate` — forzar al architect a delegar en vez de hacer él
- `/evaluate-design` — forzar ronda de evaluación de diseño
- `/reset` — context reset estructurado (escribe estado, compacta, relee todo)

## Estructura de carpetas

### Reutilizables (escritorio)
```
~/Desktop/Vibe Coding/
├── Agentes/           ← 6 .md maestros
├── commands/          ← 3 slash commands
├── design-systems/    ← Un design system por marca/proyecto
├── workflows/         ← Documentos de proceso
└── prompts/           ← Prompts reutilizables
```

### Global (una vez por ordenador)
```
~/.claude/
├── settings.json      ← Permisos, Agent Teams
├── skills/            ← Skills (react-best-practices, humanizer, etc.)
├── plugins/           ← Superpowers, code-simplifier
└── channels/telegram/ ← Token del bot
```

### Por proyecto
```
~/proyecto/
├── .claude/
│   ├── agents/        ← 6 agentes (copiados de Vibe Coding)
│   └── commands/      ← 3 comandos (copiados de Vibe Coding)
├── CLAUDE.md          ← Contexto del proyecto (corto, ~1K tokens)
├── DESIGN-SYSTEM.md   ← Identidad visual del proyecto
├── GEMINI.md          ← Copia de CLAUDE.md
├── misc/
│   ├── strategy/      ← Strategy briefs
│   ├── design/
│   │   ├── ux/        ← Specs de flujos
│   │   ├── ui/        ← Specs visuales
│   │   ├── previews/  ← HTML interactivos para aprobar
│   │   └── references/← Screenshots de inspiración
│   ├── review/        ← Audits, QA reports, evaluaciones
│   └── coding-team/   ← Task briefs
└── src/               ← Código
```

## Workflow: proyecto nuevo

```bash
# 1. Crear y estructurar
mkdir ~/proyecto && cd ~/proyecto
mkdir -p .claude/agents .claude/commands misc/strategy misc/design/ux misc/design/ui misc/design/previews misc/design/references misc/review

# 2. Copiar agentes y comandos
cp ~/Desktop/Vibe\ Coding/Agentes/*.md .claude/agents/
cp ~/Desktop/Vibe\ Coding/commands/*.md .claude/commands/

# 3. Crear CLAUDE.md (corto: qué es, qué resuelve, para quién)
# 4. Crear o copiar DESIGN-SYSTEM.md
# 5. cp CLAUDE.md GEMINI.md
# 6. Copiar archivos de referencia del proyecto
# 7. uipro init --ai claude

# 8. Git + GitHub
git init && git add -A && git commit -m "setup inicial"
gh repo create nombre --private --source=. --push

# 9. Arrancar
claude --dangerously-skip-permissions --channels plugin:telegram@claude-plugins-official
```

## Workflow: flujo de trabajo

```
@architect coordina todo
→ @designer investiga + diseña flujos + produce HTML previews
→ @design-evaluator puntúa (loop GAN hasta ≥7.0)
→ Yo apruebo el diseño
→ @developer implementa
→ @reviewer revisa código + cuestiona decisiones
→ @developer corrige
→ @qa-tester prueba como usuario real
→ @developer corrige bugs
→ Deploy
```

## Workflow: modo nocturno

```bash
caffeinate -s &  # Impedir que Mac duerma
```
Prompt: "Modo autónomo nocturno. No esperes aprobación. Trabaja seguido.
Spawna @reviewer y @qa-tester. Corrige via @developer. Commit todo.
Prepara deploy pero NO despliegues. Avísame por Telegram."

## Problemas conocidos y soluciones

### El architect no delega
Causa: context rot — instrucciones pierden peso con el tiempo.
Solución: `/delegate`, `/reset` cada hora, reglas en CLAUDE.md.

### Diseño mediocre / genérico
Causa: Claude optimiza para "correcto", no para "memorable".
Solución: loop GAN, DESIGN-SYSTEM.md con alma (filosofía + mood + anti-patrones),
skills de diseño, referencias visuales, feedback exigente.
Clave: decirle qué NO hacer es más potente que decirle qué hacer.

### Context rot (pierde el hilo)
Causa: el contexto se degrada con la longitud de la conversación.
Solución: `/reset` periódico. Escribir estado → compactar → releer instrucciones.

### Telegram se desconecta
Es experimental. Reiniciar con `--channels`.

### Auth de Claude Code expira
Escribir `/login` dentro de Claude Code.

### Mac se duerme mientras trabaja
`caffeinate -s &` antes de dejarlo solo.

## Principios que he aprendido

### Sobre CLAUDE.md
- Corto (~1K tokens). Problemas de negocio, no detalles técnicos.
- Diseño visual separado en DESIGN-SYSTEM.md.
- Incluir reglas de delegación al final.
- Protegerlo: nunca dejar que agentes lo modifiquen.

### Sobre diseño
- Mockups antes que código. Siempre.
- El loop evaluador es obligatorio — diseño nunca pasa directo a código.
- DESIGN-SYSTEM.md necesita alma, no solo tokens de color.
- Screenshots de referencia > descripciones textuales.
- Si el evaluador da 8 a todo, recalibrarlo.

### Sobre agentes
- 6 agentes es el sweet spot. Más = más coordinación, menos resultados.
- 2 Opus (designer, design-evaluator) + 4 Sonnet (el resto) para ahorrar tokens.
- El architect tiende a hacer cosas él mismo — vigilar siempre.
- Separar generador de evaluador (artículo Anthropic harness design).

### Sobre context engineering
- Contexto = recurso finito con rendimientos decrecientes.
- /reset cada hora o entre fases.
- Skills = "contexto bajo demanda" (se cargan solo cuando son relevantes).
- Tools deben ser mínimos y sin solapamiento.
- "Find the smallest set of high-signal tokens" (Anthropic).

### Sobre el proceso
- Describe problemas, no soluciones — los agentes proponen.
- "Aprobado" es la única señal para avanzar.
- Commits frecuentes antes de cada fase.
- No tener miedo de empezar de cero — el aprendizaje se acumula.
- Si algo se hace dos veces, convertirlo en skill o command.

## Artículos de referencia
- Anthropic: "Effective context engineering for AI agents"
- Anthropic: "Harness design for long-running apps"
- Boris Cherny: cómo usa Claude Code (5 en paralelo, CLAUDE.md compartido, plan mode)
- Obra Superpowers: TDD para skills, subagent-driven-development
- Addy Osmani: "The Code Agent Orchestra" (multi-agent patterns)

## Cómo prefiero que me hables
- En español
- Sin asumir conocimiento técnico
- Directo y práctico — dame los comandos, no solo la teoría
- Si algo puede salir mal, avísame antes
- Cuando me des código, dime exactamente dónde ejecutarlo
- Si pregunto algo que ya resolvimos, recuérdamelo brevemente
