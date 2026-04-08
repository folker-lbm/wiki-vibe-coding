---
tags: [claude-code, features, channels, batch, hooks, agent-teams]
sources: [10 hidden Claude code features that 99.9% ignore.md]
created: 2026-04-08
updated: 2026-04-08
---

# 10 Hidden Claude Code Features

**Source:** 10 hidden Claude code features that 99.9% ignore.md
**Date ingested:** 2026-04-08
**Type:** article (X thread)
**Author:** [[@defileo]]

## Summary

Listado de 10 features de Claude Code que la mayoría de usuarios desconoce, extraídas de la documentación oficial (hooks reference, channels page, experimental flags). Van más allá del uso básico y cambian fundamentalmente lo que Claude Code puede hacer.

## Key Claims

- [[Claude Code Features Avanzadas|Channels]] permite recibir mensajes de Telegram/Discord/iMessage dentro de una sesión activa de Claude, con contexto completo
- `/batch` lanza 5-30 agentes paralelos en worktrees aislados, cada uno abre su propio PR
- [[Claude Code Features Avanzadas|Agent Teams]] (`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`) permite equipos donde los agentes hablan entre sí, no solo con el usuario
- `/init` con `CLAUDE_CODE_NEW_INIT=1` ejecuta un setup multi-paso: escanea codebase, identifica build/tests, pregunta gaps, propone CLAUDE.md
- Hook `TaskCompleted` puede vetar que Claude marque una tarea como completada (exit code 2)
- Hook `CwdChanged` auto-recarga env (direnv) cuando Claude cambia de directorio en un monorepo
- Hook `FileChanged` con matcher reacciona a cambios en archivos específicos (ej: security audit en package-lock.json)
- `/loop` puede programar skills recurrentes: `/loop 20m /simplify focus on the auth module`
- Subagentes pueden tener memoria persistente en disco (`memory: user → ~/.claude/agent-memory/`)
- Comentarios HTML en CLAUDE.md son stripped del contexto — permiten notas para humanos sin gastar tokens

## Entities Mentioned

- [[@defileo]] — autor del hilo

## Concepts Covered

- [[Claude Code Features Avanzadas]] — features documentadas pero poco usadas
- [[Claude Code Features Avanzadas|Hooks Avanzados]] — TaskCompleted, CwdChanged, FileChanged
- [[Claude Code Features Avanzadas|Agent Teams]] — equipos multi-agente con comunicación entre sí
- [[optimizacion-tokens|Optimización de Tokens]] — HTML comments para no gastar contexto
