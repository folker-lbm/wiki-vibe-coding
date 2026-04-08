---
tags: [claude-cowork, computer-use, background-agent, seo]
sources: ["My Chief of SEO, Claude Cowork.md", "The Claude Features Nobody Talks About (But Everyone Is Paying For).md"]
created: 2026-04-08
updated: 2026-04-08
---

# Claude Cowork

Claude Cowork es el modo de trabajo en background donde Claude puede abrir apps, navegar el browser, rellenar spreadsheets, y ejecutar workflows multi-paso de forma autónoma.

## Cómo funciona

- Funciona vía Chrome extension + Claude Desktop
- Claude puede abrir cualquier tab del browser incluyendo herramientas con login (Ahrefs, SEMrush, GSC)
- **Dispatch**: asignar tareas desde el móvil, encontrar el trabajo completado en el desktop al volver
- Research preview — todavía en fase temprana, no perfecto pero funcional

## Patrón: Context Loading + Prompt Library

Demostrado en el caso de uso SEO ([Source: chief-of-seo-claude-cowork.md]):

1. **Context loading primero**: cargar todo el contexto del dominio (negocio, competidores, keywords, herramientas) en un solo prompt inicial. Sin esto, output genérico
2. **Prompt library**: prompts especializados que asumen el contexto ya cargado. Un fichero por tarea
3. **Ejecución secuencial**: prompts ordenados de quick wins a long-term (semanas 1-12)

> "Once this is loaded, every prompt you run gets sharper. Claude stops answering a stranger's question and starts answering yours." [Source: chief-of-seo-claude-cowork.md]

## Caso de uso: SEO Local

@bloggersarvesh construyó 20 prompts que cubren:
- **GBP optimization**: categorías, atributos, reviews, posts, servicios, descripción, fotos
- **Website audit**: keyword gaps, money pages, city+service pages, GSC analysis
- **Authority**: backlinks, citations, entity optimization (Knowledge Graph)
- **Content**: gap analysis, posting patterns, monthly reporting

Análisis que antes tomaba medio día por cliente ahora toma minutos.

## Diferencia con Claude Code

| | Claude Code | Claude Cowork |
|---|------------|--------------|
| Interfaz | Terminal | Desktop + browser |
| Acceso | Codebase local | Apps del sistema + browser tabs |
| Modelo | Agentic coding | Background tasks generales |
| Input | Texto/comandos | Texto + computer vision |

Ambos incluidos en Claude Pro ($20/mes).

Ver también: [[claude-code-features-avanzadas]], [[setup]]
