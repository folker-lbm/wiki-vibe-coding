---
title: "How I stopped burning 75% of my Claude budget and saved $500/month\""
source: "https://x.com/noisyb0y1/status/2041454862425047268"
author:
  - "[[@noisyb0y1]]"
published: 2026-04-07
created: 2026-04-08
description: "You pay $20/month for Pro or $100 for Max or $200 for Max 20x.And 75% of that money goes nowhere. Not to your tasks - to Claude talking to i..."
tags:
  - "clippings"
---
You pay $20/month for Pro or $100 for Max or $200 for Max 20x.

And 75% of that money goes nowhere. Not to your tasks - to Claude talking to itself. And you let it do that.

I tracked my usage for a week. Most tokens were just burned into the void. Here's what I changed to save roughly $500 a month.

## Part 1 - Teach Claude to talk like a caveman

**Regular Claude on a web search task:** ~180 tokens. It says "I'll help you search for that!" then searches, then explains what it found, then summarizes, then asks if you need anything else.

**Caveman Claude on the same task:** ~45 tokens. "Tool work , result, me stop."

135 tokens × 20 tasks a day = 2,700 saved tokens every day. Per month that's ~81,000 tokens you're no longer burning.

caveman - one skill that cuts 65-87% of token costs (1,900+ stars)

> [github.com/JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)

**Real benchmarks from the API:**

```plaintext
explain React re-render bug:       1180 → 159 tokens  (87% savings)
fix auth middleware:                704 → 121 tokens  (83% savings)
set up PostgreSQL connection pool: 2347 → 380 tokens  (84% savings)
implement React error boundary:    3454 → 456 tokens  (87% savings)
debug PostgreSQL race condition:   1200 → 232 tokens  (81% savings)
```

Average across 10 tasks: 7**5% savings**.

```python
/plugin marketplace add JuliusBrussee/caveman
/plugin install caveman
```

**Three intensity levels:**

![Image](https://pbs.twimg.com/media/HFNOpdpaQAEb4QF?format=jpg&name=large)

> lite -> removes fluff, keeps grammar (professional, no filler) full -> removes articles, fragments (full grunt mode) ultra -> maximum compression (telegraph style, cuts everything)

Start with lite. Switch to full for agentic tasks where you're not reading the responses anyway.

Why it works: caveman Claude doesn't explain itself - it just does the task. Gives the result then stops. No "I'd be happy to help." minimum fluff

**Result:** a clear short answer to your question that saves both time and tokens

![Image](https://pbs.twimg.com/media/HFNO1M1WwAAUdS1?format=jpg&name=large)

**Replaces:** Manually writing "be concise" in every prompt. how did i find this here: [https://t.me/noisyclub01](https://t.me/noisyclub01)

## Part 2 - Stop losing 2-4 hours every morning

You start working at 8:30am and already hit the limit by 11, blocked until 1:00pm. Two dead hours in the middle of your workday.

> you can game it very easily if you know the timings

**How the window actually works**

Claude usage runs on a sliding 5-hour window. The window starts when you send your first message, rounded to the hour.

> First message at 8:30 -> window anchors at 8:00 -> runs until 13:00 Hit limit at 11:00 -> wait until 13:00 -> 2 dead hours

But if you send a throwaway "hi" via Haiku at 6:15am before starting work:

"hi" at 6:15 -> window anchors at 6:00 -> runs until 11:00 At 11:00 window resets immediately Next window: 11:00 - 16:00 -> zero downtime

![Image](https://pbs.twimg.com/media/HFNOkJcWgAAyBoS?format=jpg&name=large)

Same total budget. Just distributed better across the day.

claude-warmup - automatic window anchor

> [github.com/vdesimone/claude-warmup](https://github.com/vdesimone/claude-warmup)

GitHub Actions cron job that sends "hi" to Haiku every morning. Fork it, add your OAuth token, set the schedule, done.

```python
# .github/workflows/warmup.yml
on:
  schedule:
    - cron: '15 6 * * 1-5'  # 6:15am on weekdays
git clone https://github.com/vdesimone/claude-warmup
# add CLAUDE_TOKEN to GitHub secrets
# enable Actions -> done
```

Works on Pro, Max 5x, Max 20x.

Don't want a repo? Use Claude's built-in scheduled tasks:

```python
/schedule "send 'hi' to haiku at 6:15 AM every weekday"
```

**Replaces:** Losing 2 hours every morning waiting for the window to reset.

## Part 3 - Other leaks you're probably ignoring

Edit, don't reply

When Claude misunderstands, most people write "No, I meant X." Every new message stacks on top of all previous ones. Claude re-reads the entire history every time.

```plaintext
5 messages:   7.5K tokens
10 messages:  27.5K tokens
20 messages:  105K tokens
30 messages:  232K tokens  ← message 30 costs 31x more than message 1
```

Hit Edit on your original message, fix it, regenerate. The bad exchange gets replaced not stacked.

![Image](https://pbs.twimg.com/media/HFNPc7OboAA6Dgn?format=jpg&name=large)

**Batch your questions**

> Three separate prompts = three full context loads. One prompt with three questions = one load.

**Instead of:**

```plaintext
"Summarize this article"         → wait
"Now list the main points"       → wait
"Now suggest a headline"         → wait
```

**Write:**

```plaintext
"Summarize this article, list the main points,and suggest a headline."
```

Fewer reloads. Further from the limit. Answers are usually better - Claude sees the full picture at once.

Upload files to Projects once

Uploading the same PDF to multiple chats? Claude re-tokenizes it every time.

Projects: upload once -> cached. Every conversation inside the project references it without burning tokens.

> 100-page PDF = ~75,000 tokens. Uploaded 5 times = 375,000 tokens burned. In Projects - 75,000 once, the rest is free.

Use Projects. Upload once -> cached. Contracts, briefs, style guides - this alone can save $15-40/month.

Save your context in Memory

Every new chat without saved context = 3-5 setup messages. "I'm a developer, I want short answers, always use TypeScript..."

> 5 messages × 500 tokens × 10 new chats a day = 25,000 tokens/day repeating the same thing.

Go to Settings -> Memory. Save your role and preferences once. Claude applies them to every new chat automatically. Zero setup tokens.

## Full cheatsheet

```plaintext
TOKEN KILLER #1: Chatty responses
FIX:      caveman skill → 65-87% reduction
INSTALL:  /plugin marketplace add JuliusBrussee/caveman

TOKEN KILLER #2: Morning window starts too late
FIX:      claude-warmup → anchor window at 6:00
INSTALL:  github.com/vdesimone/claude-warmup

TOKEN KILLER #3: Follow-up instead of Edit
FIX:      hit Edit → fix the prompt → regenerate

TOKEN KILLER #4: Separate questions one at a time
FIX:      batch everything into one message

TOKEN KILLER #5: Re-uploading files
FIX:      use Projects for repeated documents

TOKEN KILLER #6: Repeating context every chat
FIX:      Settings → Memory → save once
```

**Total:** up to $500+/month in leaks you can plug in 15 minutes.

> One more thing: if you're not in the US - peak hours (5:00 - 11:00 Pacific) burn through limits faster since March 2026. Run heavy tasks in the evening or on weekends - your plan stretches much further.

Claude doesn't count messages. It counts tokens. Stop giving it reasons to use more.

**You build your own life - so choose the right path. / If this was useful - follow /** more info in my tg channel**:** [https://t.me/noisyclub01](https://t.me/noisyclub01)