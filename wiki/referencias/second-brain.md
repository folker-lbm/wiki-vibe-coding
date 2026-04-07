# Second Brain — Sistema de Knowledge Base con IA

Método popularizado por Karpathy y documentado por @NickSpisak_. Es exactamente el patrón que usa esta wiki: carpetas planas + archivos markdown + un agente IA que mantiene todo organizado.

## Fuentes
- [Part 1: How to Build Your Second Brain](../../raw/How%20to%20Build%20Your%20Second%20Brain.md) — @NickSpisak_ (2026-04-04)
- [Part 2: Your Second Brain System (Done For You)](../../raw/Part%202%20Your%20Second%20Brain%20System%20(Done%20For%20You).md) — @NickSpisak_ (2026-04-04)

## Estructura base (Karpathy)

```
vault/
  raw/          ← material sin procesar
  wiki/         ← IA mantiene esto
    sources/    ← resumen por fuente
    entities/   ← personas, tools, empresas
    concepts/   ← ideas, frameworks
    synthesis/  ← comparaciones y análisis
    index.md
    log.md
  output/       ← reportes y respuestas
  CLAUDE.md     ← reglas del sistema
```

## Las 4 operaciones

1. **Onboarding** — setup inicial (una vez)
2. **Ingest** — procesar fuente nueva → actualizar wiki (una fuente toca ~10-15 páginas)
3. **Query** — preguntar contra la wiki, guardar síntesis como páginas permanentes
4. **Lint** — health check mensual: links rotos, contradicciones, huérfanos, claims sin fuente

## Ideas clave

- **Dedicated > General**: un vault por dominio, no uno gigante para todo. 40 páginas especializadas > 200 páginas mezcladas.
- **Compounding loop**: cada fuente nueva refina el wiki existente. Cada pregunta genera síntesis que alimenta futuras consultas.
- **El schema lo es todo**: CLAUDE.md define las reglas. Sin él, el agente no sabe cómo organizar.
- **No overengineer tools**: Karpathy usa "super simple and flat" — carpetas y .md. Obsidian con 47 plugins es la trampa de Notion.
- **Errores también compound**: si el IA escribe algo incorrecto y se guarda, las siguientes respuestas construyen sobre el error → lint regular es crítico.

## Casos de uso sugeridos

| Vault | Raw típico | Preguntas tipo |
|-------|-----------|----------------|
| Competitive Intel | reportes de mercado, lanzamientos | "¿Qué ha lanzado [competidor] en 90 días?" |
| Salud personal | analíticas, notas médicas | "¿Qué mejora según mis últimos 3 análisis?" |
| Cliente | transcripciones, docs proyecto | "¿Qué quedó pendiente en las últimas 3 reuniones?" |
| Learning | notas de cursos, docs, charlas | "¿Qué conceptos aparecen en 3+ fuentes sin sintetizar?" |
| Content Pipeline | drafts, analytics, competidores | "¿Sobre qué debería escribir ahora?" |

## Relación con este proyecto

Esta wiki (wiki-vibe-coding) ya implementa este patrón: `raw/` → agente IA → `wiki/`. Las diferencias principales con la propuesta de NickSpisak_:
- No usamos subcarpetas `sources/entities/concepts/synthesis/` — estructura más plana
- No tenemos `output/` separado (todavía)
- El lint/health check es manual, no automatizado con slash commands

Ver también: [[estructura]], [[principios]], [[flujo-de-trabajo]]
