# Problemas Conocidos y Soluciones

## El architect no delega
**Causa:** context rot — instrucciones pierden peso con el tiempo.
**Solución:** `/delegate`, `/reset` cada hora, reglas en CLAUDE.md. Ver [[agentes]] y [[principios]].

## Diseño mediocre / genérico
**Causa:** Claude optimiza para "correcto", no para "memorable".
**Solución:** loop GAN con threshold 8.5, DESIGN-SYSTEM.md con alma (filosofía + mood + anti-patrones), skills de diseño, referencias visuales, feedback exigente.
**Clave:** decirle qué NO hacer es más potente que decirle qué hacer.

## Context rot (pierde el hilo)
**Causa:** el contexto se degrada con la longitud de la conversación.
**Solución:** `/reset` periódico. Escribir estado → compactar → releer instrucciones.

## Telegram se desconecta
Es experimental. Reiniciar con `--channels`. Ver [[setup]] para config completa.

## Tokens se agotan demasiado rápido
**Causa:** output verboso, contexto acumulado, window mal alineada.
**Solución:** ver [[optimizacion-tokens|Optimización de Tokens]] — caveman skill, editar vs responder, window anchoring, batching.

## Auth de Claude Code expira
Escribir `/login` dentro de Claude Code.

## Wiki con información incorrecta
**Causa:** el lint detecta errores estructurales pero no de contenido. Error compounding — si algo incorrecto se guarda, las siguientes respuestas construyen sobre el error.
**Solución:** corregir en raw/ y re-ingestar. Lint mensual + cross-check manual de claims críticos. Ver [[second-brain|Second Brain]] para más sobre error compounding.

## Mac se duerme mientras trabaja
`caffeinate -s &` antes de dejarlo solo. Ver [[modo-nocturno]].
