# Equipo de Agentes

Guardados en `~/Desktop/Vibe Coding/Agentes/`. Se copian a cada proyecto nuevo.

## Los 6 agentes

| Agente | Modelo | Rol |
|--------|--------|-----|
| @architect | Sonnet | Team lead. Coordina. NUNCA ejecuta. |
| @designer | Opus | Research + UX + UI + HTML previews |
| @design-evaluator | Opus | Puntúa diseño con 4 criterios. Loop GAN. |
| @developer | Sonnet | Full-stack. Implementa y despliega. |
| @reviewer | Sonnet | Code review + devil's advocate |
| @qa-tester | Sonnet | Prueba la app como usuario real |

**Distribución de modelos:** 2 Opus (designer, design-evaluator) + 4 Sonnet (el resto) para ahorrar tokens.

## El loop evaluador (GAN)

El @designer genera, el @design-evaluator puntúa. Si <7.0, vuelve al designer. Máximo 5 rondas. Basado en el artículo de Anthropic sobre harness design.

### 4 criterios de evaluación

- **Design Quality (30%)** — coherencia visual, identidad
- **Originality (25%)** — decisiones creativas vs template
- **Craft (15%)** — tipografía, spacing, color, responsive
- **Functionality & Architecture (30%)** — usabilidad, flujos, jerarquía, escalabilidad

**Nota:** Si el evaluador da 8 a todo, recalibrarlo.

## Agent Teams (experimental)

Con `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` (ya configurado en [[setup]]), se pueden crear equipos donde los agentes **hablan entre sí**, no solo con el usuario. Comparten task list y se envían mensajes directamente.

```
Create a team: one on UX, one on architecture, one playing devil's advocate on my new auth flow
```

Se puede requerir que cada teammate presente plan para aprobación antes de escribir código. [Source: 10-hidden-claude-code-features.md]

### Sub-agent architecture (internals)

Cada sub-agent tiene contexto aislado y no puede mutar el estado del parent. Los que modifican código obtienen su propio **git worktree** (branch `worktree-<slug>`) con symlink de `node_modules`. 3 backends: in-process, tmux pane, remote. Coordinación via file-based locking. [Source: claude-code-harness-architecture.md]

Ver también: [[claude-code-arquitectura]], [[claude-code-features-avanzadas]]

## 3 slash commands

Guardados en `~/Desktop/Vibe Coding/commands/`.

- `/delegate` — forzar al architect a delegar en vez de hacer él
- `/evaluate-design` — forzar ronda de evaluación de diseño
- `/reset` — context reset estructurado (escribe estado, compacta, relee todo)
