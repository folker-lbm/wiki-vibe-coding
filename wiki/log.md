# Log

- **2026-04-07** — Ingestión inicial: `raw/CONTEXTO-LUKA-GENERIC.md` descompuesto en 9 páginas wiki (5 areas, 3 workflows, 1 referencia).
- **2026-04-07** — Ingestión: `raw/$1MYear Prediction Market Business...` → `ideas/prediction-market-infrastructure.md`
- **2026-04-07** — Ingestión: `raw/How to Build Your Second Brain.md` + `raw/Part 2 Your Second Brain System...` → `referencias/second-brain.md`

## 2026-04-07 lint | Health check
Found 0 errors, 3 warnings, 4 info items. Fixed: W1 (paths en second-brain.md), W2 (dedup agentes/principios), W3 (cross-refs en 5 páginas huérfanas).

## 2026-04-08 ingest | Batch de 7 fuentes sobre Claude Code, tokens, second brain, Cowork, prediction markets
Procesadas 7 fuentes de raw/. Saltadas 3 (1 duplicado, 2 poco sustanciales).
Creadas 11 páginas nuevas: 7 sources, 4 concepts. Actualizadas 5 páginas existentes.

**Sources creadas:**
- sources/10-hidden-claude-code-features.md ← "10 hidden Claude code features that 99.9% ignore.md"
- sources/claude-code-harness-architecture.md ← "How I built harness for my agent using Claude Code leaks.md"
- sources/claude-budget-optimization.md ← "How I stopped burning 75% of my Claude budget and saved $500month.md"
- sources/karpathy-second-brain-guide.md ← "karpathy's second brain how to build it.md"
- sources/chief-of-seo-claude-cowork.md ← "My Chief of SEO, Claude Cowork.md"
- sources/claude-features-nobody-talks-about.md ← "The Claude Features Nobody Talks About (But Everyone Is Paying For).md"
- sources/polymarket-bot-mistakes.md ← "Why your Claude bot doesn't work.md"

**Concepts creados:**
- concepts/claude-code-arquitectura.md — 4 capas, async generator, compactación, permisos, retry
- concepts/claude-code-features-avanzadas.md — channels, /batch, agent teams, hooks, /loop
- concepts/optimizacion-tokens.md — caveman, window anchoring, prompt cache, budgeting
- concepts/claude-cowork.md — background agent, computer use, context loading pattern

**Páginas actualizadas:**
- areas/agentes.md — añadido Agent Teams y sub-agent architecture
- areas/setup.md — añadido Channels, Hooks avanzados, plugin Caveman
- areas/principios.md — añadido prompt cache design, compactación jerárquica, harness vs infrastructure
- referencias/second-brain.md — añadido datos del gist, otros practicantes (Fridman, Saravia), tabla de limitaciones
- ideas/prediction-market-infrastructure.md — añadido errores comunes del bot y thresholds

## 2026-04-08 lint | Health check
Found 0 errors, 3 warnings, 3 info items. All fixed:
- W1: 14 wikilinks rotos → 6 concept links redirigidos con pipe syntax, 8 entity links convertidos a texto plano, accent mismatches corregidos
- W2: 3 páginas huérfanas → cross-refs añadidos (proyecto-nuevo desde flujo-de-trabajo, prediction-market-infrastructure desde principios, articulos desde principios)
- W3: casing inconsistente → estandarizado con `[[slug|Display Name]]`
- I1: cross-ref añadido entre claude-budget-optimization y 10-hidden-claude-code-features
- I2: data gaps documentados (MCP, Gemini CLI, /batch workflows)
- I3: second-brain.md "Relación con este proyecto" actualizado (ya no dice que no usamos subcarpetas)

**Saltadas:**
- "$1MYear Prediction Market Business — Built With Claude bot 1.md" (duplicado del ya ingerido)
- "Thread by @RoundtableSpace.md" (poco sustancial — solo /powerup y reacciones)
- "Thread by @mrmagan_.md" (poco sustancial — micro-thread sobre second brain + NYT infographics)
