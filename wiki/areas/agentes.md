# Equipo de Agentes

Guardados en `~/Desktop/Vibe Coding/Agentes/`. Se copian a cada proyecto nuevo.

## Los 6 agentes

| Agente | Modelo | Rol |
|--------|--------|-----|
| @architect | **Opus** | Team lead. Coordina. NUNCA ejecuta. |
| @designer | **Opus** | Research + UX + UI + HTML previews |
| @design-evaluator | **Opus** | Puntúa diseño con 4 criterios. Loop GAN. |
| @developer | **Sonnet** | Full-stack. Implementa y despliega. |
| @reviewer | **Opus** | Code review + devil's advocate |
| @qa-tester | **Sonnet** | Prueba la app como usuario real |

**Distribución de modelos:** 4 Opus (architect, designer, design-evaluator, reviewer) + 2 Sonnet (developer, qa-tester).

## El loop evaluador (GAN)

El @designer genera, el @design-evaluator puntúa. Si <8.5, vuelve al designer. Máximo 5 rondas. Basado en el artículo de Anthropic sobre harness design.

### 4 criterios de evaluación (pesos correctos)

| Criterio | Peso |
|----------|------|
| Design Quality | 30% |
| Originality | 25% |
| Craft | 15% |
| Functionality | 30% |

### Rangos de puntuación

- **<6.0: FAIL** — replanteamiento total
- **6.0-8.4: ITERATE** — vuelve al designer con feedback específico
- **≥8.5: PASS** — listo para aprobación del usuario

**Threshold: 8.5/10** — el diseño debe ser destacable, no solo correcto.

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
