---
tags: [tokens, optimización, costes, caveman, prompt-cache]
sources: ["How I stopped burning 75% of my Claude budget and saved $500month\".md", "How I built harness for my agent using Claude Code leaks.md", "The Claude Features Nobody Talks About (But Everyone Is Paying For).md"]
created: 2026-04-08
updated: 2026-04-08
---

# Optimización de Tokens

Técnicas para reducir el consumo de tokens en Claude, tanto en uso interactivo como en agent loops.

## Output: Reducir verbosidad

### Caveman Skill
Reduce output tokens **65-87%**. Claude responde sin fluff: resultado y para.

```
/plugin marketplace add JuliusBrussee/caveman
```

| Tarea | Sin caveman | Con caveman | Ahorro |
|-------|------------|-------------|--------|
| Explain React re-render bug | 1,180 | 159 | 87% |
| Fix auth middleware | 704 | 121 | 83% |
| Setup PostgreSQL connection pool | 2,347 | 380 | 84% |

3 niveles: **lite** (sin filler, gramática ok), **full** (fragmentos, grunt mode), **ultra** (estilo telegrama). Lite para trabajo normal, full para tareas agentic donde no lees las respuestas.

> Repo: github.com/JuliusBrussee/caveman (1,900+ stars) [Source: claude-budget-optimization.md]

### HTML Comments en CLAUDE.md
Comentarios `<!-- -->` se stripean del contexto. Notas para humanos sin gastar tokens. [Source: 10-hidden-claude-code-features.md]

## Input: Reducir contexto cargado

### Editar vs Responder
Cada mensaje nuevo re-lee todo el historial. Crecimiento exponencial:
- 5 msgs = 7.5K tokens
- 20 msgs = 105K tokens
- 30 msgs = 232K tokens (**31x** más que el primero)

**Fix**: editar el mensaje original y regenerar, no escribir "No, quise decir X".

### Batching
3 preguntas separadas = 3 cargas de contexto completas. 1 prompt con 3 preguntas = 1 carga. Las respuestas suelen ser mejores porque Claude ve el panorama completo.

### Projects
Subir PDFs/docs una vez → cached. 100 páginas = 75K tokens. Subido 5 veces en chats diferentes = 375K desperdiciados. En Projects = 75K una vez, el resto gratis.

### Memory Settings
Guardar rol y preferencias en Settings → Memory. Evita 25K tokens/día de setup repetido (5 msgs × 500 tokens × 10 chats nuevos).

## Rate Limits: Window Anchoring

La ventana de uso es de **5 horas deslizantes**, anclada a la hora en punto del primer mensaje.

```
Primer mensaje 8:30 → ventana 8:00-13:00 → hit limit 11:00 → blocked hasta 13:00 (2h muertas)
```

**Fix**: enviar "hi" a Haiku a las 6:15am:
```
"hi" 6:15 → ventana 6:00-11:00 → reset 11:00 → siguiente ventana 11:00-16:00 → 0 downtime
```

Automatizable con:
- `claude-warmup`: GitHub Actions cron job (github.com/vdesimone/claude-warmup)
- `/schedule "send 'hi' to haiku at 6:15 AM every weekday"` (nativo)

> Peak hours (5:00-11:00 Pacific) gastan más rápido desde marzo 2026. Tareas pesadas mejor en evening/weekends. [Source: claude-budget-optimization.md]

## Arquitectura: Prompt Cache

Del análisis de Claude Code ([Source: claude-code-harness-architecture.md]):

- System prompt dividido en zona estática (~80%, cache hit global) y zona dinámica
- Contexto de usuario inyectado como primer user message, no en system prompt → no rompe cache
- Diferencia entre $0.02 y $0.20 por sesión a escala

## Arquitectura: Tool Result Budgeting

- Cada tool define `maxResultSizeChars`
- Resultados grandes → disco. Modelo recibe file path + preview
- `applyToolResultBudget()` limita total de tokens de tool results por API call

Ver también: [[claude-code-arquitectura]], [[principios]], [[setup]]
