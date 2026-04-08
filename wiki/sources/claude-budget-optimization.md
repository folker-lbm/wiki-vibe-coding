---
tags: [claude, tokens, optimización, presupuesto, caveman]
sources: ["How I stopped burning 75% of my Claude budget and saved $500month\".md"]
created: 2026-04-08
updated: 2026-04-08
---

# Claude Budget Optimization

**Source:** How I stopped burning 75% of my Claude budget and saved $500month".md
**Date ingested:** 2026-04-08
**Type:** article (X thread)
**Author:** [[@noisyb0y1]]

## Summary

Guía práctica para reducir el gasto de tokens en Claude. El autor rastreó su uso una semana y encontró que el 75% de tokens se desperdiciaba en output verboso e ineficiencias de conversación. Presenta fixes concretos con benchmarks reales.

## Key Claims

- **Caveman skill** reduce output tokens 65-87% — Claude responde sin fluff, solo resultado y para
  - Benchmarks: "explain React re-render bug" 1180→159 tokens (87%), "fix auth middleware" 704→121 (83%)
  - 3 niveles: lite (sin filler), full (fragmentos), ultra (estilo telegrama)
  - Repo: github.com/JuliusBrussee/caveman (1,900+ stars)
- **Window anchoring**: la ventana de uso es de 5 horas deslizantes, se ancla a la hora en punto del primer mensaje. Enviar "hi" a Haiku a las 6:15am ancla la ventana a 6:00, evitando 2h de downtime al mediodía
  - claude-warmup: GitHub Actions cron job que lo automatiza
  - También funciona con `/schedule` nativo de Claude
- **Editar vs responder**: cada mensaje nuevo re-lee todo el historial. 5 msgs=7.5K tokens, 30 msgs=232K tokens (31x más). Editar el mensaje original y regenerar ahorra exponencialmente
- **Batching**: 3 preguntas separadas = 3 cargas de contexto completas. 1 prompt con 3 preguntas = 1 carga
- **Projects**: subir PDFs una vez y reutilizar (100 páginas = 75K tokens; subido 5 veces = 375K desperdiciados)
- **Memory settings**: guardar rol y preferencias una vez, evita 25K tokens/día de setup repetido
- Peak hours (5:00-11:00 Pacific) gastan más rápido desde marzo 2026

## Entities Mentioned

- [[@noisyb0y1]] — autor
- **Caveman** (JuliusBrussee) — skill de compresión de output

## Concepts Covered

- [[optimizacion-tokens|Optimización de Tokens]] — reducción de gasto en Claude
- [[Claude Code Features Avanzadas]] — /schedule para warmup

Ver también: [[10-hidden-claude-code-features|10 Hidden Claude Code Features]] para más técnicas de ahorro (HTML comments en CLAUDE.md).
