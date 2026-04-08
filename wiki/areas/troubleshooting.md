# Problemas Conocidos y Soluciones

## El architect no delega
**Causa:** context rot — instrucciones pierden peso con el tiempo.
**Solución:** `/delegate`, `/reset` cada hora, reglas en CLAUDE.md. Ver [[agentes]] y [[principios]].

## Diseño mediocre / genérico
**Causa:** Claude optimiza para "correcto", no para "memorable".
**Solución:** loop GAN, DESIGN-SYSTEM.md con alma (filosofía + mood + anti-patrones), skills de diseño, referencias visuales, feedback exigente.
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

## Mac se duerme mientras trabaja
`caffeinate -s &` antes de dejarlo solo. Ver [[modo-nocturno]].
