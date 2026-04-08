# Prediction Market Infrastructure — "Sell Shovels"

**Fuente:** [@kirillk_web3](https://x.com/kirillk_web3/status/2037192322660655132) (2026-03-23)

## Tesis central
No ganes dinero prediciendo. Gana dinero vendiendo herramientas a los que predicen. Infraestructura > trading.

> "You trade → you win sometimes, lose sometimes. You build the infrastructure → you profit from every trader using it."

## El patrón histórico
- Gold rush: los que vendían palas se hicieron ricos, no los mineros.
- Internet: sistemas de pago y CDNs superaron a la mayoría de webs.
- Crypto: exchanges e infraestructura ganaron más que los traders.
- Prediction markets: mismo patrón, ventana abierta ahora.

## Modelo de negocio: Automation as a Service

### Productos posibles
- **Bot subscriptions** — bots listos con parámetros configurables
- **Copy-trading dashboards** — auto-seguir estrategias de los mejores traders
- **Market scanners** — detección de anomalías e ineficiencias en tiempo real
- **Execution engines** — sistemas de alto rendimiento para traders serios
- **Analytics dashboards** — probabilidades, volumen, liquidez, top traders

### Pricing
| Tier | Precio | Target |
|------|--------|--------|
| Bot subscriptions | $200–500/mes | Mass market |
| Private tools | $1,000–5,000/mes | Traders serios |
| Automation dashboards | $5,000–10,000 setup + mensual | Equipos y fondos |
| Institucional | $10,000+/mes | Enterprise |

### Matemáticas
- 150 traders × $300/mes = $540K/año
- 5 clientes privados × $2,000/mes = +$120K/año
- 1 cliente institucional × $10,000/mes = +$120K/año
- **Total conservador: $780K/año**

## Nichos con más potencial para automatización
- **Crypto (BTC/ETH):** señal externa limpia (Binance), alta frecuencia, ineficiencias constantes
- **Sports (NFL, NBA, soccer, MLB, tennis):** datos de lesiones y alineaciones infrautilizados — las odds de Polymarket van 5-10 min detrás
- **Weather:** modelos meteorológicos (NOAA, ECMWF) actualizan más rápido que Polymarket
- **Política/elecciones:** alto volumen ($500M+ en ciclos electorales)
- **Indicadores económicos:** Fed, desempleo, inflación — calendario predecible

## Cómo se construye (playbook)
1. **Elegir un nicho** — especificidad > universalidad
2. **Estudiar patrones del mercado** — velocidad de reacción, liquidez, duración de ineficiencias
3. **Convertir el patrón en código** — monitorizar feeds → detectar lag → auto-entrar → auto-salir
4. **Convertirlo en infraestructura** — de script a producto
5. **Monetizar** — subscripciones escalonadas

## Relevancia para vibe coding
El artículo menciona Claude como capa de desarrollo: describes la lógica de trading y Claude genera la arquitectura, conexiones API, scripts de monitoreo y lógica de ejecución. Lo que antes requería semanas de ingeniería ahora se prototipa en horas.

## Stack mencionado
- **Claude** — inteligencia/desarrollo
- **Composio** — capa de integración (250+ APIs con auth gestionado)
- **Polymarket API** — mercados
- **Telegram/Slack/Discord** — notificaciones

## Errores comunes al construir el bot

Follow-up del artículo original con 12M views ([Source: polymarket-bot-mistakes.md]):

- **Errores 1-3**: impiden que el bot funcione (credenciales, API, environment)
- **Errores 4-6**: producen resultados incorrectos (datos stale, edge mal calculado)
- **Errores 7-9**: destruyen la cuenta gradualmente (sin risk management)

### Thresholds antes de ir live
- 200+ trades completados en paper mode
- Win rate >75% en paper
- 7 días consecutivos sin crashes
- Desplegado en VPS (no laptop)

### Setup crítico
- Credenciales en `.env`, nunca hardcodeadas. `.gitignore` antes de todo
- Alchemy RPC (no public RPC) para transacciones en Polygon
- Paper mode por defecto con 3 flags para live: `--live --confirm --i-understand-risks`
- Risk management no-negociable: halt diario (-20%), halt permanente (60% ATH), pausa tras 5 pérdidas consecutivas

> "La diferencia entre bots que ganan dinero y los que no, no es la estrategia — es la calidad de ejecución." [Source: polymarket-bot-mistakes.md]

Ver también: [[setup]] para stack de vibe coding disponible.
