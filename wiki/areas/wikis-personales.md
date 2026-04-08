---
tags: [second-brain, obsidian, wiki, workflow]
sources: [CONTEXTO-LUKA-GENERIC.md]
created: 2026-04-08
updated: 2026-04-08
---

# Wikis Personales (Segundo Cerebro)

Sistema basado en el patrón [[second-brain|LLM Wiki de Karpathy]] (abril 2026). Cada wiki es un repo público en GitHub mantenido por un agente IA. Ver [[estructura]] para la estructura de carpetas.

## Wikis activas

| Wiki | GitHub | Contenido |
|------|--------|-----------|
| wiki-vibe-coding | github.com/folker-lbm/wiki-vibe-coding | Agentic coding, Claude Code, agentes, workflows |
| wiki-personal | github.com/folker-lbm/wiki-personal | Diario, ideas, filosofía, economía, trading |

## Loop diario

1. Encuentras algo interesante → Obsidian Web Clipper → `raw/`
2. `wiki` (alias en terminal) → `/second-brain-ingest`
3. Para consultar: pregunta en lenguaje natural
4. Mensual: `/second-brain-lint`

## Herramientas

- **Obsidian** — visor de las wikis (grafo de conceptos, navegación por wikilinks)
- **Obsidian Web Clipper** — extensión Chrome para clipear artículos directamente a `raw/`
- **second-brain skill** — 4 comandos para gestionar las wikis. Ver [[setup]]

## Alias de terminal

```bash
alias wiki="cd ~/wiki-vibe-coding && claude"
```

## Principios

- Una wiki por dominio — no mezclar. Ver [[principios]].
- Corregir siempre en `raw/`, nunca en la wiki directamente.
- El agente escribe `wiki/`, el humano escribe `raw/`.

Ver también: [[wiki-brain]] para la app web que da acceso sin terminal.
