---
title: "The Claude Features Nobody Talks About (But Everyone Is Paying For)"
source: "https://x.com/zodchiii/status/2041448674115424392"
author:
  - "[[@zodchiii]]"
published: 2026-03-31
created: 2026-04-08
description: "Here are the features most people don't know exist.Most people type a question, get an answer, close the tab and pay Claude $20/month for a ..."
tags:
  - "clippings"
---
Most people type a question, get an answer, close the tab and pay Claude $20/month for a chatbot.

There are features built into Claude right now that most users have never clicked, never enabled, and in some cases never even seen.

If you're paying for Claude and only chatting with it, this article is the list of everything you're missing 👇

Before we dive in, I share daily notes on AI & vibe coding in my Telegram channel: [https://t.me/zodchixquant](https://t.me/zodchixquant) 🧠

![Image](https://pbs.twimg.com/media/HFSstqPb0AAxmCn?format=jpg&name=large)

## 1\. Projects

**What it is:** Persistent workspaces where Claude remembers everything you upload and every instruction you give, across all conversations in that project.

**Why most people miss it:** They use Claude as one-off conversations. Ask a question, get an answer, start a new chat. All context is lost.

**How to actually use it:** Create a Project for each area of your work or life. Upload documents, write custom instructions, and every conversation inside that project has full context without you repeating yourself.

```text
Example Projects you can set up in 5 minutes:

"Content" → upload your writing style guide, past articles, tone examples
"Work" → upload current priorities, meeting notes, project docs  
"Research" → upload papers, articles, notes on your topic
"Code" → upload your architecture docs, API specs, tech stack info
"Clients" → upload contracts, briefs, communication history
```

The difference is massive.

Instead of explaining who you are and what you need every single conversation - Claude already knows.

It's the difference between talking to a stranger every time and working with someone who's been on your team for months.

![Image](https://pbs.twimg.com/media/HFSs7ZGWoAEvGWs?format=jpg&name=large)

## 2\. Deep Research

**What it is:** Claude spends several minutes actively searching the web, reading dozens of sources, cross-referencing information, and producing a structured report with citations.

**Why most people miss it:** It's a separate button in the bottom left of the chat interface. If you've never clicked it, you've never seen what it can do.

**How to actually use it:** Click the Research button (bottom left, turns blue when active), then ask a detailed research question. Claude will run for 3-10 minutes and come back with something that would take you half a day to assemble manually.

Regular web search pulls a few results and summarizes them.

Deep research breaks your question into sub-tasks, runs multiple searches in parallel, reads full articles, cross-references claims, and synthesizes everything into a structured report with links.

```text
Regular search:

"What's happening with AI regulation?"
→ Generic 3-paragraph summary

Deep research:  

"Compare the EU AI Act, US executive orders, and China's AI 
regulations as of 2026. For each, cover scope, enforcement 
mechanisms, impact on startups, and key differences."
→ Structured report with cited sources, 5-10 minutes of research
```

> Take a look at official Anthropic's walkthrough of deep research.

> Worth watching before you try it yourself: 👇

<video preload="none" tabindex="-1" playsinline="" aria-label="Embedded video" poster="https://pbs.twimg.com/amplify_video_thumb/2041446846606815232/img/fxo9s5Yhe6Q4p-0w.jpg" style="width: 100%; height: 100%; position: absolute; background-color: black; top: 0%; left: 0%; transform: rotate(0deg) scale(1.005);"><source type="video/mp4" src="blob:https://x.com/69c9bb26-be45-4b7e-92c1-96d107c306aa"></video>

![](https://pbs.twimg.com/amplify_video_thumb/2041446846606815232/img/fxo9s5Yhe6Q4p-0w.jpg?name=large)

## 3\. Artifacts

**What it is:** Claude can create standalone files, interactive code, visualizations, documents, and web apps directly in the chat. They render in a preview panel next to the conversation.

**Why most people miss it:** They ask Claude to "write code" and copy-paste the output. They don't realize Claude can build something you can actually see, click, and interact with right there in the chat.

**How to actually use it:** Ask Claude to create something visual or interactive. It generates an Artifact that renders live next to your conversation. You can iterate on it, download it, or share it.

```text
Things Claude can build as Artifacts:

- Interactive dashboards and calculators
- SVG diagrams and charts
- Full React components that work in the browser
- Formatted documents (markdown, HTML)
- Presentations and slide decks
- Data visualizations from your data
- Working prototypes and mini-apps
```

I use this constantly for banners, data visualizations, and interactive tools. Instead of opening Canva or Figma, I describe what I want and Claude builds it in the chat.

Not perfect for everything, but for quick visuals it's faster than any dedicated tool.

![Image](https://pbs.twimg.com/media/HFStXVJbAAAoZoa?format=jpg&name=large)

## 4\. Memory

**What it is:** Claude remembers things about you across conversations. Your preferences, your projects, your communication style, decisions you've made, context from previous chats.

**Why most people miss it:** It works in the background. You might not even realize Claude is using memory unless you check Settings.

**How to actually use it:** Go to Settings → Memory and look at what Claude already remembers about you. Edit anything wrong, add context it should know, and delete anything you don't want it to remember.

The more accurate your memory profile, the less you repeat yourself. Claude starts adapting to you without being asked because it remembers that you prefer concise answers, that you work in fintech, that your team uses React, or whatever else it's picked up from your conversations.

If you're switching from ChatGPT, there's an import feature that lets you bring your conversation history and preferences over so you don't start from zero.

![Image](https://pbs.twimg.com/media/HFStbNdXoAAFdJf?format=png&name=large)

## 5\. Styles

**What it is:** Saved tone and formatting presets that apply across conversations. Instead of writing "be concise, use bullet points, no fluff" every time, you save it as a style and select it.

**Why most people miss it:** It's tucked away in settings and most people don't know it exists.

**How to actually use it:** Create different styles for different contexts. One for work emails (professional, concise), one for blog posts (conversational, detailed), one for code reviews (technical, direct). Select the style before you start chatting and Claude automatically follows it.

```text
Example styles:

"Work" → Professional tone, concise, no fluff, suggest next steps
"Writing" → Conversational, opinionated, use examples, avoid AI-sounding phrases  
"Technical" → Precise, use jargon, include code examples, be thorough
"Quick" → Maximum 3 sentences, no preamble, direct answer only
```

This is one of the smallest features on this list but it saves the most daily friction.

![Image](https://pbs.twimg.com/media/HFStgdVaEAA93Uf?format=jpg&name=large)

## 6\. Web Search

**What it is:** Claude searches the internet in real-time and cites its sources. Not just training data from months ago, but what's actually on the web right now.

**Why most people miss it:** It used to be turned off by default. Some people still don't know it's there.

**How to actually use it:** Toggle web search on (bottom of the chat input, next to the other tools). Now Claude can answer questions about current events, recent news, live data, and anything that's changed since its training data was collected.

For anything time-sensitive, web search should always be on.

![Image](https://pbs.twimg.com/media/HFStjvKbkAAJOtr?format=jpg&name=large)

## 7\. Code Execution

**What it is:** Claude can actually run code, not just write it. It executes Python, JavaScript, and other languages right in the chat and shows you the output.

**Why most people miss it:** They see code blocks in Claude's responses and think "okay, I'll copy this into my IDE." They don't realize Claude already ran it and can show them the result.

**How to actually use it:** Ask Claude to analyze data, create visualizations, or run calculations. It writes the code, executes it, and shows you the output. No copy-pasting, no switching tools, no "let me run this real quick."

```text
What code execution unlocks:

- "Analyze this CSV and show me trends" → runs pandas, shows charts
- "Calculate compound interest for these scenarios" → runs the math, shows results  
- "Parse this JSON and extract the fields I need" → runs the script, gives you clean output
- "Convert this data from format A to format B" → runs the conversion, gives you the file
```

This is the feature that turns Claude from "an AI that writes code" to "an AI that runs code for you." Huge difference.

![Image](https://pbs.twimg.com/media/HFStpGAXQAECAFj?format=jpg&name=large)

## 8\. File Creation

**What it is:** Claude can create and export actual files. Word documents, Excel spreadsheets, PowerPoint presentations, PDFs, code files. Real files you can download and use immediately.

**Why most people miss it:** They ask Claude to "write a report" and copy-paste the text into their own document. They don't know they can just say "create a Word doc" and get a downloadable file.

**How to actually use it:** Just ask for the file type you want. "Create a PowerPoint presentation about X." "Build me an Excel spreadsheet with these columns and formulas." "Generate a PDF report." Claude creates the file and you download it.

For anyone who spends time formatting documents, building spreadsheets, or creating presentations, this feature alone justifies the $20/month.

A slide deck that would take you an hour to build in PowerPoint takes Claude about 2 minutes.

![Image](https://pbs.twimg.com/media/HFStum8XUAAb7SN?format=jpg&name=large)

## 9\. Claude Code

**What it is:** A terminal-based coding agent that reads your entire codebase, writes code, runs commands, manages git, and ships features. It works from your terminal, not from the browser.

**Why most people miss it:** It requires opening a terminal and typing claude. Most non-developers don't know it exists, and many developers don't know it's included in their Pro subscription.

**How to actually use it:** Install it with **npm install -g**[@anthropic](https://x.com/@anthropic)**\-ai/claude-code**, open your terminal in a project directory, and type **claude**. It reads your codebase and you can start giving it tasks in plain English.

This is a separate product that deserves its own article (I wrote one: Top 20 Claude Code Commands), but the key point here is that it's included in your $20/month Pro plan.

> Mar 31

You're already paying for it.

## 10\. Cowork

**What it is:** Claude works on tasks in the background while you do other things. It can open apps on your computer, navigate your browser, fill in spreadsheets, and handle multi-step workflows autonomously.

**Why most people miss it:** It launched recently and most people still think of Claude as a chat window, not a background worker.

**How to actually use it:** Open Claude Desktop, start a Cowork session, and give it a task. With Dispatch, you can even assign tasks from your phone and find the completed work on your desktop when you get back.

This is the feature that changes Claude from "a tool you talk to" into "a colleague you delegate to."

It's still in research preview and not perfect, but it already handles tasks like compiling reports, organizing files, and managing routine workflows.

![Image](https://pbs.twimg.com/media/HFSugZNb0AAAKiH?format=jpg&name=large)

## What you're actually paying for

```text
CLAUDE PRO — $20/MONTH

Feature                  What it does                           Are you using it?
──────────────────────────────────────────────────────────────────────────────────
Projects                 Persistent workspaces with memory       □
Deep Research            Multi-source cited reports               □
Artifacts                Interactive files and visualizations      □
Memory                   Remembers you across conversations       □
Styles                   Saved tone presets                       □
Web Search               Real-time internet access                □
Code Execution           Runs code and shows output               □
File Creation            Exports Word, Excel, PPT, PDF            □
Claude Code              Terminal coding agent                    □
Cowork                   Background task automation               □
```

Count your checkboxes.

If it's less than 7, you're leaving money on the table.

Most people are paying $20/month for a chatbot.

You're paying $20/month for a research assistant, a coding agent, a document creator, a background worker, and a full productivity system. The only question is whether you're actually using it.

**!**I share daily notes on AI, finance, and vibe coding in my Telegram channel: [https://t.me/zodchixquant](https://t.me/zodchixquant)**!**

![Image](https://pbs.twimg.com/media/HFSupmLb0AAqU-r?format=jpg&name=large)

Thanks for reading 🙏🏼