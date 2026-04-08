---
tags: [proyecto, wiki, app, vercel]
sources: [CONTEXTO-LUKA-GENERIC.md]
created: 2026-04-08
updated: 2026-04-08
---

# Wiki Brain

App web personal para acceder a las [[wikis-personales]] sin terminal. Desplegada en Vercel.

## Datos del proyecto

| Campo | Valor |
|-------|-------|
| Repo local | `~/wiki-chat` |
| Stack | Next.js 14, Tailwind, API Anthropic |
| Design system | Linear.app |
| Deploy | Vercel |

## Funciones

- Chat con wiki (preguntas en lenguaje natural)
- Panel lateral navegable (explorar páginas)
- Grafo de conceptos (visualización de wikilinks)
- Flashcards con repaso espaciado
- Resumen diario
- Sugerencias de conexiones

## Relación con las wikis

Wiki Brain es la capa de acceso. Las wikis siguen siendo repos Git con markdown — Wiki Brain las lee y permite interactuar con ellas desde el navegador o el móvil, sin necesidad de abrir terminal ni Obsidian.

Ver también: [[wikis-personales]], [[second-brain]]
