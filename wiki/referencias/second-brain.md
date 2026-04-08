# Second Brain — Sistema de Knowledge Base con IA

Método popularizado por Karpathy y documentado por @NickSpisak_. Es exactamente el patrón que usa esta wiki: carpetas planas + archivos markdown + un agente IA que mantiene todo organizado.

## Fuentes
- [Part 1: How to Build Your Second Brain](../../raw/How%20to%20Build%20Your%20Second%20Brain.md) — @NickSpisak_ (2026-04-04)
- [Part 2: Your Second Brain System (Done For You)](../../raw/Part%202%20Your%20Second%20Brain%20System%20(Done%20For%20You).md) — @NickSpisak_ (2026-04-04)
- [Karpathy's Second Brain Guide](../sources/karpathy-second-brain-guide.md) — @godofprompt (2026-04-02)

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

## Datos del gist original de Karpathy

El gist obtuvo 5,000+ stars y 1,400+ forks en dos días, 100K bookmarks en el post original. Karpathy generó ~100 artículos, ~400K palabras sobre un tema de investigación sin escribir una palabra. Múltiples implementaciones open-source aparecieron en GitHub en 48h. [Source: karpathy-second-brain-guide.md]

## Otros practicantes

- **Lex Fridman**: genera visualizaciones HTML interactivas y crea "mini-knowledge-bases" que carga en voice mode para correr (7-10 millas)
- **Elvis Saravia** (DAIR.AI): usa knowledge bases de LLM para curación de AI research
- **@mrmagan_**: usa el patrón para "shower thoughts" → genera investigative reports estilo NYT con infografías

## Limitaciones (la versión honesta)

[Source: karpathy-second-brain-guide.md]

| Limitación | Detalle |
|-----------|---------|
| **Context ceiling** | 128K tokens ≈ 96K palabras. IA lee selectivamente via index, puede perder cosas. Efecto "lost in the middle" |
| **Error compounding** | Error sutil → se guarda → se construye encima → 2 meses después 5 páginas refuerzan el mismo error |
| **Hallucination** | Se reduce (grounding en fuentes) pero no se elimina. El formato autoritativo hace más probable confiar en info incorrecta |
| **Coste** | Una fuente ~10-15 páginas = $2-5 API. 50 fuentes = $100-250 solo ingestión |
| **Escala** | Funciona a ~100 artículos. A 10,000+ el index crece demasiado |
| **Single-model blind spots** | Toda la wiki es interpretación de un solo modelo |

### Mitigaciones
- Lint mensual + cross-check manual de claims críticos
- Un vault por dominio (no mezclar)
- Modelos baratos para updates simples, frontier para ingest/queries complejas
- Aceptar que es herramienta personal, no enterprise
- Para decisiones críticas: correr queries en 4+ modelos y comparar

## Casos de uso sugeridos

| Vault | Raw típico | Preguntas tipo |
|-------|-----------|----------------|
| Competitive Intel | reportes de mercado, lanzamientos | "¿Qué ha lanzado [competidor] en 90 días?" |
| Salud personal | analíticas, notas médicas | "¿Qué mejora según mis últimos 3 análisis?" |
| Cliente | transcripciones, docs proyecto | "¿Qué quedó pendiente en las últimas 3 reuniones?" |
| Learning | notas de cursos, docs, charlas | "¿Qué conceptos aparecen en 3+ fuentes sin sintetizar?" |
| Content Pipeline | drafts, analytics, competidores | "¿Sobre qué debería escribir ahora?" |

## Relación con este proyecto

Esta wiki (wiki-vibe-coding) implementa este patrón: `raw/` → agente IA → `wiki/`. Ya usamos la estructura completa con subcarpetas `sources/`, `concepts/`, y las operaciones core:
- **Ingest** via `/second-brain-ingest` — procesa fuentes de `raw/` a wiki
- **Query** via `/second-brain-query` — preguntas contra la wiki
- **Lint** via `/second-brain-lint` — health check automatizado

Ver también: [[estructura]], [[principios]], [[flujo-de-trabajo]]
