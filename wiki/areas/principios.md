# Principios Aprendidos

## Sobre CLAUDE.md
- Corto (~1K tokens). Problemas de negocio, no detalles técnicos.
- Diseño visual separado en DESIGN-SYSTEM.md.
- Incluir reglas de delegación al final.
- Protegerlo: nunca dejar que agentes lo modifiquen.

## Sobre diseño
- Mockups antes que código. Siempre.
- El loop evaluador es obligatorio — diseño nunca pasa directo a código.
- DESIGN-SYSTEM.md necesita alma, no solo tokens de color.
- Screenshots de referencia > descripciones textuales.

## Sobre agentes
- 6 agentes es el sweet spot. Más = más coordinación, menos resultados.
- El architect tiende a hacer cosas él mismo — vigilar siempre.
- Ver [[agentes]] para distribución de modelos, loop GAN y criterios de evaluación.

## Sobre context engineering
- Contexto = recurso finito con rendimientos decrecientes.
- /reset cada hora o entre fases.
- Skills = "contexto bajo demanda" (se cargan solo cuando son relevantes).
- Tools deben ser mínimos y sin solapamiento.
- "Find the smallest set of high-signal tokens" (Anthropic).
- **Prompt cache design**: system prompt estático (~80%) arriba del boundary, dinámico abajo. Contexto de usuario como primer user message, no en system prompt → no rompe cache. [Source: claude-code-harness-architecture.md]
- **Compactación jerárquica**: microcompact (gratis) → snip → auto-summarize → collapse. Nunca saltar a lo caro primero. Ver [[claude-code-arquitectura]].

## Sobre harness vs infrastructure
- El harness (tools, loops, error handling) es capa 3. La capa 4 es **infrastructure**: multi-tenancy, permisos, aislamiento, persistencia, coordinación. [Source: claude-code-harness-architecture.md]
- "Teams that understand distributed systems build agents that work. Teams that stop at the harness build demos."
- CLAUDE.md tiene 4 niveles: /etc (enterprise) → proyecto → usuario → local. Es RBAC para comportamiento de agentes.
- Error recovery como estado first-class en el loop, no un try-catch exterior. Cada tipo de error tiene recovery path específico.

## Sobre el proceso
- Describe problemas, no soluciones — los agentes proponen.
- "Aprobado" es la única señal para avanzar.
- Commits frecuentes antes de cada fase.
- No tener miedo de empezar de cero — el aprendizaje se acumula.
- Si algo se hace dos veces, convertirlo en skill o command.

Ver también: [[articulos]] para lecturas de referencia, [[prediction-market-infrastructure]] como caso de estudio de vibe coding aplicado.
