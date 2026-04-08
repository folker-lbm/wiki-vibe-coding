---
tags: [polymarket, arbitraje, bot, errores, trading]
sources: ["Why your Claude bot doesn't work.md"]
created: 2026-04-08
updated: 2026-04-08
---

# Polymarket Bot — 9 Errores y Fixes

**Source:** Why your Claude bot doesn't work.md
**Date ingested:** 2026-04-08
**Type:** article (X thread)
**Author:** [[@adiix_official]]

## Summary

Follow-up a un artículo viral (12M views) sobre bots de arbitraje en Polymarket. Documenta los 9 errores más comunes que cometieron los miles de personas que intentaron construir el bot, con fixes exactos. Incluye prompt actualizado y battle-tested, plus guía de setup A-Z.

## Key Claims

- Errores 1-3 impiden que el bot funcione. Errores 4-6 producen resultados incorrectos. Errores 7-9 destruyen la cuenta gradualmente
- **Prompt actualizado** incluye: credenciales desde .env, Binance WebSocket con auto-reconnect, edge detection (mín 5% detectable, 8% ejecutable), half-Kelly para position sizing, risk management con halt automático (-20% diario, 60% de ATH, 5 pérdidas consecutivas), async architecture, Telegram alerts, paper mode por defecto con 3 flags para live
- **Setup correcto**: generar bot → environment → credentials → **7 días mínimo de paper mode** → VPS → live con posiciones pequeñas
- Thresholds de paper mode antes de ir live: 200+ trades completados, win rate >75%, 7 días sin crashes
- Usar Alchemy RPC (no public RPC) para transacciones en Polygon
- Nunca hardcodear private keys — .env + .gitignore
- La estrategia sigue funcionando pero el edge es más estrecho que en 2024

## Entities Mentioned

- [[@adiix_official]] — autor
- Polymarket — plataforma de prediction markets
- Binance — fuente de datos de precios

## Concepts Covered

- [[Prediction Market Infrastructure]] — el lado operativo de construir bots

Ver también: [[Prediction Market Infrastructure]] para la tesis completa y el playbook.
