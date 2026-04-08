---
title: "10 hidden Claude code features that 99.9% ignore"
source: "https://x.com/defileo/status/2041116337120915535"
author:
  - "[[@defileo]]"
published: 2026-04-06
created: 2026-04-08
description: "I went past the quickstart, past the common workflows, all the way to the hooks reference, the channels page, the experimental flags. The ..."
tags:
  - "clippings"
---
I went past the quickstart, past the common workflows, all the way to the hooks reference, the channels page, the experimental flags. The features there don't just save time, they change what Claude Code is:

## I / Channels: message Claude from Telegram, Discord, or iMessage while it works.

```text
claude --channels plugin:telegram@claude-plugins-official
```

Start Claude with the \`--channels\` flag and install a plugin, once set up, Claude is reachable by DM on whichever platform you choose. Your CI fails at 2 a.m, Claude gets the event pushed into its session, diagnoses the failure, and sends you a fix summary on Telegram before you wake up.

You reply with “do it” and it applies the fix.

This is not polling, it’s not a webhook to a new session. The event arrives in the Claude session that’s already open, with full context.

Telegram, Discord, and iMessage are the three supported platforms, it requires a claude ai login, not an API key.

## II / /batch: one command, 5-30 parallel agents, one PR each

Type /batch followed by any large-scale instruction and Claude breaks the codebase into independent units, asks for approval, then spawns one isolated agent per unit in a separate git worktree.

```text
/batch migrate src/ from Solid to React
```

Each agent implements its piece, runs tests, and opens a pull request. You get back a stack of PRs, not a 4000-line diff, the work happens in parallel, so you don't babysit any of it.

This is a bundled skill, so it's available in every session. Most people have never typed /batch.

## III / Agent teams: teammates that talk to each other, not just to you

Enable with one env variable, then ask Claude to create a team and describe the roles.

```text
CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

```text
Create a team: one on UX, one on architecture, one playing devil's advocate on my new auth flow
```

Unlike subagents, which only report back to you, teammates share a task list and message each other directly. One finds a security issue and tells the architecture teammate, that teammate revises the plan. The devil's advocate pushes back and you watch it play out and jump in when needed.

You can require each teammate to submit a plan for approval before writing a single line.

You set the criteria: "only approve plans that include test coverage." The lead enforces it.

## IV / /init with CLAUDE\_CODE\_NEW\_INIT=1: Claude interviews your codebase, then you

Most people run /init once and get a basic CLAUDE.md, enable this flag first and the whole thing changes.

```text
CLAUDE_CODE_NEW_INIT=1
```

Claude runs a multi-step setup flow.

It scans your codebase, identifies build commands, tests, and architecture, then asks a few questions to fill the gaps, before changing anything, it shows you a proposal to review.

You get a CLAUDE.md tailored to how your project actually works, so future sessions start with Claude already knowing your rules.

## V / TaskCompleted hook: a shell script that can veto Claude calling its own work done

Hooks fire at specific points in the agent lifecycle, most people know about PreToolUse, BUT! Almost nobody configures TaskCompleted.

```text
TaskCompleted → your script runs → exit 2 to block it
```

Exit with code 2, and your message goes back to Claude: "tests are still failing, task is not done" Claude keeps working and you never had to be watching

Pair it with TaskCreated to reject tasks that don’t meet your standards before they even start. This is quality enforcement baked into the agent loop itself, not a prompt you hope Claude follows.

## VI / CwdChanged hook: auto-reload your env when Claude changes directories

This hook fires whenever Claude executes a cd command, the docs call out its use case directly: reactive environment management with direnv.

```text
CwdChanged → trigger direnv reload
```

You’re in a monorepo, Claude moves into packages/payments to work on the billing module, and the environment variables for that package load automatically.

Claude moves to packages/auth, different vars, reloaded automatically.

No more broken sessions because Claude is running commands in the wrong environment.

## VII / FileChanged hook: Claude reacts when a file changes on disk

The matcher field tells this hook which filenames to watch, when one changes, by anything, not just Claude, the hook fires.

```text
FileChanged (matcher: "package-lock.json") → run security audit
```

Your dependency lock file changes, Claude automatically runs a dependency audit. Your config file changes, Claude re-validates it, A generated file changes, Claude checks whether the source is still in sync.

This turns Claude from something you prompt into something that watches your project and responds.

## VIII / THIS ESPECIALLY USEFUL ONE: /loop that re-runs other skills: schedule any skill on an interval

Most people know /loop for polling, what the docs show is that the scheduled prompt can be another skill invocation.

```text
/loop 20m /simplify focus on the auth module
```

Every 20 minutes, Claude runs your /simplify skill on the current state of the auth module and reports back. Your PR review skill, security checker, documentation linter, any of them can be set on a timer while you work on something else.

Skills composing with scheduling, it’s in the docs tho almost nobody does it.

## IX / Subagent persistent memory: your agents remember things across sessions

When creating a custom subagent, you can enable a persistent memory directory. The subagent writes what it learns to disk and loads it at the start of every future session.

```text
memory: user  →  ~/.claude/agent-memory/
```

Your code reviewer catches your recurring async error-handling mistakes and remembers them. Next session, it’s already up to speed, your debugger tracks your common failure patterns. Your data analyst sticks to your preferred outputs.

That’s the difference between a tool you have to re-teach every time and one that learns you.

## X / HTML comments in CLAUDE.md: notes that load for humans but not Claude

CLAUDE.md is loaded into the context window every session, every line costs tokens. But standard HTML block comments are stripped before the file is injected into context.

```text
<!-- Last reviewed: March 2025. Update auth section after OAuth migration. -->
```

You can leave maintainer notes, change history, explanations of why a rule exists, none of it hits the context window, Claude never sees it, ur teammates do when they open the file.

This is documented in a single sentence in the memory page, almost nobody noticed it.