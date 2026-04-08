---
tags: [claude-code, arquitectura, harness, infrastructure, agent-loop]
sources: [How I built harness for my agent using Claude Code leaks.md]
created: 2026-04-08
updated: 2026-04-08
---

# Claude Code Harness Architecture

**Source:** How I built harness for my agent using Claude Code leaks.md
**Date ingested:** 2026-04-08
**Type:** article (X thread)
**Author:** [[@rohit4verse]]

## Summary

Análisis profundo de la arquitectura de Claude Code (55 dirs, 331 módulos). El autor argumenta que el framework real tiene 4 capas (no 3): Weights → Context → Harness → **Infrastructure**. Documenta cada decisión arquitectónica: el agent loop como async generator, tool concurrency classification, streaming tool executor, prompt caching, 4 estrategias de compactación, 7 stages de permisos, sistema de retry de 823 líneas, y sub-agent architecture con git worktree isolation.

## Key Claims

- El framework real de agentes tiene **4 capas**: Weights, Context, Harness, Infrastructure (multi-tenancy, RBAC, aislamiento, persistencia, coordinación distribuida)
- SWE-agent (Princeton NLP) demostró 64% de mejora cambiando solo la interfaz, no el modelo
- El agent loop en `query.ts` (1,729 líneas) es un **async generator** (`async function*`), no un while loop — permite streaming, cancelación, composabilidad y backpressure
- Cada iteración pasa por **5 fases**: Setup → Model Invocation → Error Recovery & Compaction → Tool Execution → Continuation Decision
- Tools se clasifican por concurrencia: read-only (Glob, Grep, Read) en paralelo (hasta 10), write (Bash, Edit, Write) en serie → 2-5x speedup
- **StreamingToolExecutor** ejecuta tools durante el streaming, antes de que el modelo termine de generar
- Tool result budgeting: resultados grandes se persisten a disco, el modelo recibe solo preview + file path
- System prompt dividido en zona estática (cacheable globalmente, ~80%) y zona dinámica — diseñado para cache efficiency
- Contexto de usuario inyectado como primer user message (no system prompt) para no romper el cache
- **4 estrategias de compactación**: Microcompact (cada turno, ~0 coste) → Snip (corta inicio) → Auto (summariza) → Context Collapse (compresión multi-fase)
- Sistema de permisos de **7 stages** con pipeline cascading: enterprise → project → user → session
- CLAUDE.md tiene **4 niveles**: /etc (enterprise/MDM) → proyecto (.claude/) → usuario (~/.claude/) → local (CLAUDE.local.md)
- Sistema de retry: 823 líneas, maneja 10+ clases de error, cada una con recovery path específico
- Sub-agentes en **git worktrees** aislados, con symlink de node_modules para no duplicar
- 3 backends de ejecución: in-process, tmux pane, remote (CCR)
- Coordinación de tareas con file-based locking y exponential backoff (30 retries, 5-100ms)

## Entities Mentioned

- [[@rohit4verse]] — autor del análisis
- Princeton NLP — SWE-agent paper
- Anthropic — creador de Claude Code

## Concepts Covered

- [[Claude Code Arquitectura]] — las 4 capas y decisiones de diseño
- [[Claude Code Arquitectura|Context Compaction]] — 4 estrategias ordenadas por coste
- [[optimizacion-tokens|Optimización de Tokens]] — prompt cache boundary, tool result budgeting
- [[Claude Code Features Avanzadas|Agent Teams]] — sub-agent architecture, worktree isolation
