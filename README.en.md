# ai-project-context-pattern

> A methodology for turning your project into a self-growing knowledge base when you vibe code with AI.

[中文](README.md) | **English**

## What it is
If you vibe code with AI, here's a way to turn your project into a **self-growing knowledge base** — the AI captures and maintains knowledge a bit every conversation, so it gets richer over time instead of being rebuilt from scratch every time (RAG).

It works via two layers of **progressive disclosure**: a base layer `AGENTS.md` (at the project root, auto-loaded) holding maintenance rules + a full navigation index; and a reveal layer `wiki/` read on demand, holding the project's own knowledge. Knowledge **compounds** — cross-references, flagged contradictions, and syntheses are all prepared in the wiki, ready to use.

## Who it's for
- **Good fit**: solo developers, or tightly-knit small teams (roughly 2-5 people), vibe coding with AI.
- **Not a good fit**: as an enterprise knowledge-management system — it has no permissions / approval / provenance, and multiple teams writing the same wiki concurrently will clash.
- Key point: the **read side** (looking up project context) benefits teams of any size; the **write side** (maintaining the wiki) is what's constrained by headcount. Small teams can use it — treat wiki edits like code (PR review + split ownership).

## Structure
```
project root/
├── AGENTS.md            ← auto-loaded: maintenance rules + positioning + index (navigation hub)
├── log.md               ← project change log
└── wiki/                ← AI-maintained knowledge
    ├── architecture/       technical architecture
    ├── decisions/          decisions (ADRs: why we decided X)
    ├── bugs/               bug postmortems
    ├── sessions/           session archives (on demand, after summarization)
    └── *.md                other knowledge (concepts / how-tos)
```

## How to use
Paste the prompt below to your AI (works with opencode / Claude Code / Cursor / Aider). It fetches the methodology doc and sets up a knowledge base for your project **in English**:

```
Set up an AI-maintained knowledge base for this project using the "AI Project Context Pattern".

Doc URL (fetch and read in full, then follow its own process):
https://raw.githubusercontent.com/EggsAndTomato/ai-project-context-pattern/refs/heads/master/ai-project-context-pattern.md

Ask me about anything unclear first; don't start writing until confirmed.
```

> The methodology doc is in Chinese, but it's written for the AI to read and instructs the AI to generate in **your language** — since this prompt is in English, your knowledge base will be in English.

## This repo is itself an example
This repo maintains its own knowledge base with its own methodology (`AGENTS.md` + `wiki/`) — i.e., dogfooding; feel free to use it as a reference.

## Inspiration
Inspired by Andrej Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — having the LLM incrementally build and maintain a persistent wiki rather than retrieving from raw docs every time (RAG). This repo applies that idea to organizing **project** context.

---
Full methodology (Chinese, for the AI to read): [`ai-project-context-pattern.md`](ai-project-context-pattern.md)
