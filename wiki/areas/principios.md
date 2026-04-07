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
- Si el evaluador da 8 a todo, recalibrarlo.

## Sobre agentes
- 6 agentes es el sweet spot. Más = más coordinación, menos resultados.
- 2 Opus (designer, design-evaluator) + 4 Sonnet (el resto) para ahorrar tokens.
- El architect tiende a hacer cosas él mismo — vigilar siempre.
- Separar generador de evaluador (artículo Anthropic harness design).

## Sobre context engineering
- Contexto = recurso finito con rendimientos decrecientes.
- /reset cada hora o entre fases.
- Skills = "contexto bajo demanda" (se cargan solo cuando son relevantes).
- Tools deben ser mínimos y sin solapamiento.
- "Find the smallest set of high-signal tokens" (Anthropic).

## Sobre el proceso
- Describe problemas, no soluciones — los agentes proponen.
- "Aprobado" es la única señal para avanzar.
- Commits frecuentes antes de cada fase.
- No tener miedo de empezar de cero — el aprendizaje se acumula.
- Si algo se hace dos veces, convertirlo en skill o command.
