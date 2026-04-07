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

## 3 slash commands

Guardados en `~/Desktop/Vibe Coding/commands/`.

- `/delegate` — forzar al architect a delegar en vez de hacer él
- `/evaluate-design` — forzar ronda de evaluación de diseño
- `/reset` — context reset estructurado (escribe estado, compacta, relee todo)
