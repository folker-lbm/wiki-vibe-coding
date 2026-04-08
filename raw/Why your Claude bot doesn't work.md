---
title: "Why your Claude bot doesn't work"
source: "https://x.com/adiix_official/status/2041455811671564747"
author:
  - "[[@adiix_official]]"
published: 2026-04-07
created: 2026-04-08
description: "A complete guide to the arbitrage bot and how you can build your own with Claude. After 12 million views, thousands of people tried to build..."
tags:
  - "clippings"
---
A complete guide to the arbitrage bot and how you can build your own with Claude. After 12 million views, thousands of people tried to build the arbitrage bot. Most failed. Here are the 9 mistakes they made and the exact fixes, step by step.

![Image](https://pbs.twimg.com/media/HFSxex2bMAAmo1m?format=jpg&name=large)

# What happened after 12 million people read part one

The first article got 12 million views. Thousands of people copied the prompt, opened Claude, and started building their own Polymarket arbitrage bot. Then the DMs started coming in.

"My bot generates but never places a trade." "The API keeps throwing 401 errors." "It runs in paper mode fine but crashes when I go live." "I've been running it for three days and the win rate is 34%." "Claude wrote the code but I can't figure out how to actually run it."

Every single one of these problems is fixable. Every single one of them also has a specific cause not bad luck, not a broken platform, not a defective model. A fixable mistake in setup, configuration, or strategy that happens at a predictable point in the process.

This article documents all nine of them. For each one: what the mistake is, why it happens, what it looks like when it's happening to you, and the exact fix.

**Before you read further:** If you haven't read the original article How Claude turned $300 into $2,382,780 start there. This guide assumes you understand how latency arbitrage works and have already attempted to build a bot. If you're starting from zero, part one is the foundation.

[https://x.com/adiix\_official/status/2037604599398322682](https://x.com/adiix_official/status/2037604599398322682)

# How to build your own from A to Z

Everything that follows is a complete operational guide. If you follow each step in sequence and don't skip the risk management setup, you'll have a running bot by the end of the day. If you skip steps especially step 4 and step 5 you will lose money. That's not a hedge. It's just what happens.

## • Set up a Polymarket wallet

Go to [Polymarket](https://polymarket.com/?r=ecosystem) and connect MetaMask or Coinbase Wallet. Fund it with USDC via the Polygon network not Ethereum mainnet, not any other chain. Polygon is the network Polymarket runs on, and using the wrong network means your funds sit inaccessible. For testing purposes, $100–300 is sufficient. For real trading with meaningful compounding, start with $500–1,000. **Important: Polymarket is not available to US residents.** If you're in the US, you cannot legally access the platform. Check the legal status in your specific country before depositing anything.

## • Generate your API credentials

Go to [docs.polymarket.com](https://docs.polymarket.com/), navigate to the API section, and generate a CLOB API key by signing a message with your wallet. This proves ownership without requiring a password. You'll also need your wallet's private key to sign individual trade transactions. Store this private key in a local environment variable **never hardcode it into your bot script, never commit it to GitHub, never share it with anyone.** A leaked private key means a drained wallet. This is the one step where operational security genuinely matters.

# The 9 mistakes diagnosed and fixed

These are ordered by how early in the process they occur. Mistakes 1–3 prevent the bot from running at all. Mistakes 4–6 let it run but produce wrong results. Mistakes 7–9 let it run and produce results, but destroy the account over time.

![Image](https://pbs.twimg.com/media/HFSwaC9bIAAi030?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSwe66bEAA1c7q?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSwkvOXMAAsVH_?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSwrE0XcAAaZSy?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSwwrFXQAAYAiZ?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSw2I7a8AA8nb4?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSxpK5bIAAINir?format=jpg&name=large)

Profile:[https://polymarket.com/@0x8dxd?r=0x8dx](https://polymarket.com/@0x8dxd?r=0x8dx)

![Image](https://pbs.twimg.com/media/HFSx-JRbQAAiKe2?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSx86_W0AA_etv?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSyDaXW8AArm5S?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSyIMiXQAEnqp8?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSyL54XwAAEG3h?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSyP_3aAAAy-o5?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSyXmNXgAAJxcY?format=jpg&name=large)

# Wrong vs right the full comparison

Here is the complete picture of what a broken setup looks like versus a working one. Use this as a reference checklist before you go live.

![Image](https://pbs.twimg.com/media/HFSylaxbcAA3NQg?format=jpg&name=large)

# The correct prompt updated and battle-tested

After seeing what broke in thousands of real attempts, here is the updated prompt. It incorporates all nine fixes from the start so you don't have to patch them in afterwards.

Copy this verbatim. Do not simplify it. Every line is there for a reason.

Build me a production-ready Python latency arbitrage bot for Polymarket with ALL of the following requirements: CREDENTIALS: - Load all keys from a .env file using python-dotenv - Never hardcode credentials in the script - Required env vars: POLY\_API\_KEY, POLY\_PRIVATE\_KEY, TELEGRAM\_TOKEN, TELEGRAM\_CHAT\_ID, ALCHEMY\_RPC\_URL PRICE MONITORING: - Connect to Binance WebSocket: wss://stream.binance.com:9443 - Track BTC/USDT and ETH/USDT ticker streams - Auto-reconnect on disconnect with exponential backoff (max 10 retries) - Reject price data older than 10 seconds as stale - Pause all trading when price data is stale EDGE DETECTION: - Minimum detectable edge: 5% (ignore anything below) - Minimum execution edge: 8% (only trade above this) - Only monitor BTC/ETH contracts, 5-minute and 15-minute duration - Minimum market liquidity: $50,000 - Maximum 20 markets monitored simultaneously POSITION SIZING: - Use half-Kelly Criterion for every position - Hard cap: maximum 8% of current portfolio per trade - Recalculate portfolio value before every trade RISK MANAGEMENT (non-negotiable): - Daily halt if P&L falls below -20% of day-start balance - Permanent halt if portfolio falls below 60% of all-time high - 30-minute pause after 5 consecutive losses - All halts send Telegram alert and require manual restart to resume EXECUTION: - Full async architecture (asyncio + aiohttp, no blocking calls) - Use Alchemy RPC from env var for Polygon transactions - Total execution time target: under 800ms from detection to order MONITORING: - Telegram alert on every: trade entry, trade exit, error, kill switch - Hourly heartbeat: balance, today's trades, today's win rate - Rotating log file: all activity with timestamps, 50MB max PAPER MODE: - Paper mode enabled by default - Three explicit flags required to enable live: --live --confirm --i-understand-risks - Paper mode logs all simulated trades to SQLite Use Python 3.11+. Include a requirements.txt with pinned versions. Start in paper mode. Do not enable live trading without explicit flags.

![Image](https://pbs.twimg.com/media/HFSzBORXQAAytfs?format=jpg&name=large)

## The correct setup step by step

This is the sequence that produces a working bot. Follow it in order. Do not skip steps, especially 4 and 5.

## Generate the bot with the updated prompt

Open [Claude.ai](https://claude.ai/) or Claude Code. Paste the full prompt from section 04 above verbatim, nothing removed. Claude will generate a complete Python codebase. It should include a main bot file, a requirements.txt, and a .env.example template.

If any of these are missing, ask Claude: "You didn't generate \[requirements.txt / .env.example\]. Add it." Don't proceed without all three files.

## Set up the environment

Create a project folder. Save the bot files there. Create a virtual environment with python3 -m venv bot-env and activate it. Install dependencies with pip install -r requirements.txt.

Copy .env.example to .env and fill in your credentials. Add .env to .gitignore before doing anything else.

## Get your credentials

**Polymarket API key:** Go to [docs.polymarket.com](https://docs.polymarket.com/) → API Keys → generate via your wallet signature. This authenticates your account.

**Wallet private key:** Export from MetaMask (Settings → Security → Export Private Key). This signs transactions. It must start with 0x.

**Alchemy RPC:** Create a free account at [alchemy.com](https://alchemy.com/) → Create App → Polygon Mainnet → copy the HTTPS endpoint. This replaces slow public RPC nodes.

**Telegram bot:** Message [@BotFather](https://x.com/@BotFather) on Telegram → /newbot → copy the token. Then message your bot and get your chat ID from the API.

## Run paper mode for 7 days minimum

Start the bot with python3 [bot.py](https://bot.py/) paper mode is the default. Do not modify this.

Watch the first 20–30 trades manually. Verify: the edge calculations look right, the bot is not trading on stale data, the Telegram alerts arrive correctly, the logs are writing.

**Your paper trading must hit all three before you go live:**

- At least**200 completed paper trades**
- Paper win rate above**75%**
- At least**7 consecutive days**of running without crashes

If paper mode doesn't hit these numbers, the bot has a problem. Find it before you trade real money.

## Deploy to a VPS before going live

A $5/month VPS on DigitalOcean, Linode, or Vultr gives you 24/7 uptime. Running the bot on your laptop means it stops when you sleep, travel, or restart.

Transfer your bot files (not your .env create a new one on the server). Install dependencies. Run paper mode on the VPS for 48 hours to confirm it's stable there too.

## Go live small, then scale

When paper mode passes all three thresholds and the VPS is stable, start live trading with the flags: python3 [bot.py](https://bot.py/) --live --confirm --i-understand-risks

**First week of live trading:** watch every single trade. Compare live win rate to paper win rate daily. If they diverge by more than 10%, stop and investigate before continuing.

Scale position sizes gradually only when you have 50+ live trades of data confirming the system works in real conditions.

# The debug checklist if it's still broken

If you've followed everything above and the bot still isn't working, go through this checklist in order. Every item here was a real failure point reported by readers of part one.

![Image](https://pbs.twimg.com/media/HFSzr8PWcAABYii?format=jpg&name=large)

![Image](https://pbs.twimg.com/media/HFSz198a8AAEkfW?format=jpg&name=large)

# One last thing

Every mistake in this guide was real. Someone reading part one hit each of these problems, spent time debugging it, and didn't have a resource like this. Now you do.

The arbitrage window still exists. The strategy still works. The edge is narrower than it was in 2024, but it's real and exploitable with a properly built system. The difference between the bots that make money and the bots that don't isn't the strategy it's the execution quality.

Build it right. Test it properly. Scale only when you have evidence.

Good luck and if something works, I'd genuinely love to hear about it.

**Part 3 is coming.** Advanced optimization how to get execution time under 400ms, how to run multiple bots on different strategies simultaneously, and how to handle the next wave of edge compression. Follow to get it when it drops.

[@adiix\_official](https://x.com/@adiix_official)