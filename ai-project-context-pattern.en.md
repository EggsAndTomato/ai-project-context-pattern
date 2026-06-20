# AI Wiki Context Pattern (An LLM-Maintained Project Knowledge Base)

> For individuals / small teams doing vibe coding with AI (opencode, Claude Code, etc.).
> **This document is meant to be read by the AI**: in a new project, have the AI read this, then set up the project knowledge base per "Section 8".
> Core goal: **incrementally accumulate and continuously maintain** project knowledge, rather than rediscovering it every conversation.
>
> *Note: This is an English translation of [`ai-project-context-pattern.md`](ai-project-context-pattern.md) (Chinese, canonical). If the two ever diverge, the Chinese version is authoritative.*

---

## 1. Core Idea: Incremental Accumulation + Continuous Maintenance (Anti-RAG)

The common approach is RAG: upload a batch of documents, then retrieve relevant fragments at query time and assemble an answer on the spot. The problem is **every question is rediscovered from scratch** — knowledge never accumulates. Ask something that requires synthesizing five sources, and the AI has to find and re-stitch them every single time; nothing gets deposited.

This pattern is different: **the LLM incrementally builds and maintains a persistent wiki** — a set of structured, interlinked markdown files sitting between you and the raw information. When new knowledge arrives, the AI doesn't just index it for later retrieval; it **reads it, distills the key points, and integrates it into the existing wiki**: updating related pages, revising syntheses, flagging contradictions, adding cross-references. Once knowledge is **deposited into the wiki, it stays up to date**, rather than being recomputed per question.

The key difference: **the wiki is a compounding artifact.** Cross-references are already built, contradictions already flagged, syntheses already reflect everything you've read. Every source added, every question asked, makes the wiki richer.

Division of labor: **humans handle sourcing, exploration, and asking the right questions; the LLM handles all bookkeeping** (summarizing, cross-referencing, archiving, keeping things consistent) — precisely the chores that make people abandon maintaining a knowledge base, and that an LLM never gets bored of.

---

## 2. Structure

| Layer | Location | Loading | Contents | Size target |
|---|---|---|---|---|
| Base layer | `./AGENTS.md` (**project root**) | Auto-loaded | CRITICAL maintenance rules + 1-line positioning + **index (full directory)** | ≤ ~300 lines (trim if exceeded) |
| Reveal layer | `wiki/*.md` + `log.md` | AI reads on demand | Project knowledge + change log | Unlimited; navigated via index |

```
project root/
├── AGENTS.md            ← base layer (auto-loaded)
├── log.md               ← project change log
└── wiki/
    ├── architecture/    ← fixed: technical architecture
    ├── decisions/       ← fixed: ADRs (why we decided X)
    ├── bugs/            ← fixed: bug postmortems
    ├── sessions/        ← fixed: session archives
    └── *.md             ← the rest: concepts / how-tos / domain knowledge / reference notes (LLM creates freely, interlinks)
```

> Under `wiki/`, **only these 4 subdirectories + root-level loose files are allowed**; creating other subdirectories is forbidden. Every page must be registered in the AGENTS.md index. This pattern **does not have a raw layer** (no quarantine area for immutable source material is needed).

---

## 3. Base Layer: AGENTS.md

### Must live in the project root

opencode / Claude Code only auto-load: the `AGENTS.md` in the project root (and parent directories walked upward), plus the global `~/.config/opencode/AGENTS.md`. **An AGENTS.md in a subdirectory is NOT loaded.** Put it in the wrong place = the whole pattern fails.

### Contents = Rules + Positioning + Index

AGENTS.md consists of three blocks:

1. **Top: CRITICAL maintenance rules** (tool-action-level; see Section 7 for why)
2. **Project positioning**: 1 line (including tech-stack keywords)
3. **Index**: the full wiki directory, grouped by the 4 fixed categories + loose, one summary line per entry

> The index **lives permanently in AGENTS.md and is never externalized**. Externalizing it = turning the "navigation hub" into lazy-loaded content, which breaks the premise of this pattern. If the index bloats, **trim it** (merge fragmented entries, archive stale ones, shorten summaries) — don't split it into lazy-loaded chunks. ~300 lines is the trigger line for a "directory slimming Lint".

### AGENTS.md Template

```markdown
# {Project name}

> Positioning: {one line, including tech stack}.

<!-- ============ Maintenance rules (CRITICAL) · human-defined, LLM must not change ============ -->
## Maintenance Rules (CRITICAL)

- Before answering any substantive question: your **next action** is to read the index below in full, then decide which wiki pages to read.
- After **creating a new page** under wiki/: your **next action** is to append a row to the index below (the index is appended only in this case).
- After any **structural / intent-level change** (creating / deleting / renaming files, revising root-level docs, adjusting core terminology or decisions): your **next action** is to append an entry to `log.md` (newest on top, recording "what changed + why").
- After creating / updating a wiki page: your **next action** is to add a markdown link in that page's `## Related` section for each structurally related page, and add a backlink in the linked page's `## Related` section.
- Under wiki/, **only** 4 subdirectories (architecture/decisions/bugs/sessions) or root-level loose files are allowed; **creating other subdirectories is forbidden**.
- You **may only modify the index region of this file**; the rest of this file (rules, positioning) must not be modified.
- **Never archive raw sessions**; a session must be summarized before archiving.

<!-- ============ Project positioning · human-defined ============ -->
## Project Positioning
{one-line positioning, including tech stack}

<!-- ============ index · LLM-maintained ============ -->
## Index (full wiki directory)
### architecture
| File | Summary |
|---|---|
| `wiki/architecture/overview.md` | {one line} |

### decisions
| File | Summary |
|---|---|
| `wiki/decisions/001-xxx.md` | {one line} |

### bugs
| File | Summary |
|---|---|

### sessions
| File | Summary |
|---|---|

### Other (root-level loose)
| File | Summary |
|---|---|
| `wiki/{concept}.md` | {one line} |
```

---

## 4. Reveal Layer: wiki/ and log.md

- The **4 fixed subdirectories** hold "templated, structured artifacts"; **root-level loose files** hold the rest of the knowledge (concepts, how-tos, domain notes, references). Navigation is via index categories + **inter-document linking**.
- **Interlinking convention**: use markdown links `[text](relative-path.md)` (**not** `[[wikilinks]]`, to stay zero-tool / portable). When first mentioning an entity / decision / concept that already has an authoritative page, link to it; every structured page must have a `## Related` section. The LLM maintains these autonomously: creating pages, updating pages, adding / fixing links, keeping consistency.
- **Single source of truth**: the same knowledge is stated authoritatively in only one place; elsewhere it is only linked, never copied.
- `log.md` = project change log (structural / intent-level "what changed + why", newest on top; trivial code revisions go in git).

### Fixed subdirectories and page templates

**`architecture/` — Technical architecture page**
```markdown
# {Component / system name}

> Scope: this page covers "what it is + how it's built".

## Responsibilities
{what this component does}
## Composition and data flow
{modules, key paths, how data moves}
## Boundaries and interfaces
{internal and external contracts}
## Key constraints
{hard constraints that must not be violated}
## Related
- Decision basis: [ADR-00X: title](../decisions/00x-xxx.md)
- Runtime details: [component/concept name](../architecture/xxx.md)
```

**`decisions/` — ADR (why we decided X)**
```markdown
# ADR-{number}: {decision title}

> Date: {YYYY-MM-DD}  Status: Accepted / Deprecated / Superseded

## Background
{why this decision was needed; candidate options}
## Decision
{what was chosen}
## Rationale
{why it was chosen}
## Consequences
{costs, impact, sacrificed trade-offs}
## Related
- Related decision: [ADR-00X](00x-xxx.md)
- Affected architecture: [component name](../architecture/xxx.md)
```

**`bugs/` — Bug postmortem**
```markdown
# BUG-{number}: {one-sentence symptom}

> Date: {YYYY-MM-DD}  Status: Fixed

## Symptom
{manifestation, trigger conditions, impact}
## Investigation
{directions explored, how it was localized}
## Root cause
{the actual cause}
## Fix
{how it was fixed; measures to prevent recurrence}
## Retrospective
{lessons, whether it exposed an architectural issue, related decisions}
## Related
- Decision tied to root cause: [ADR-00X](../decisions/00x-xxx.md)
- Architecture touched by the fix: [component name](../architecture/xxx.md)
```

**`sessions/` — Session archive (after summarization)**
```markdown
# SESSION-{date}-{topic}

> Date: {YYYY-MM-DD}  Archived: {YYYY-MM-DD}

## Topic
{what this session was solving}
## Key decisions
{what was decided; which pages/ADRs it sedimented into}
## Conclusions and outputs
{summary of code / page changes}
## Next steps
{unfinished, TODOs}
## Related
- Sedimented decisions: [ADR-00X](../decisions/00x-xxx.md)
- Architecture / bugs touched: [page name](../architecture/xxx.md)
```

---

## 5. Three Operations: Ingest / Query / Lint

**Ingest (take in new knowledge).** New knowledge arrives (read a doc, understood a concept, made a decision) → the LLM writes / updates the relevant pages → **updates the index** → **appends to the log**. One ingest may touch multiple pages.

**Query (ask).** Before answering, scan the index to locate relevant pages, then read, synthesize, and cite. **A good answer can be archived as a new page** — a comparison you did, an analysis, a connection you spotted; don't let it vanish in chat, let it keep compounding.

**Lint (self-healing net · required).** Periodically have the LLM health-check the wiki and fix:
- Pages contradicting each other
- Orphan pages (no incoming links)
- Dangling links (pointing to deleted / renamed / nonexistent files)
- One-way links (A→B but B's `## Related` doesn't link back)
- Missing cross-references (an entity / decision with an authoritative page is mentioned but not linked)
- Index missing an entry / index has an entry whose file no longer exists
- Stale claims (superseded by new knowledge but not updated)
- Important concepts mentioned repeatedly without their own page
- AGENTS.md exceeding ~300 lines → run a directory slimming

> Lint is **required**, not optional. Because behavioral instructions like "update the index/log" will inevitably be violated occasionally (see Section 7), Lint is the self-healing net for "imperfect compliance" — it detects drift and repairs it.

---

## 6. Session Archiving Discipline

`sessions/` is archived **on demand**, not every time:
- **The user explicitly asks to archive**, or
- **The LLM judges the session important and prompts the user whether to archive.**

Before archiving, **you must summarize first** (distill per the sessions template: topic / key decisions / conclusions / next steps); **raw session records are never stored**. Important decisions should simultaneously sediment into `decisions/` (ADRs) and `log.md`; the session page keeps only the narrative of "what happened in that session".

> This effectively turns "session-output sedimentation discipline" into a fixed directory, rather than banning archiving — it gives summarized, on-demand sessions a proper home.

---

## 7. Why CRITICAL + Tool-Action-Level Rules

Empirical fact: **"loaded into context" ≠ "followed."** Plain behavioral rules (especially ones requiring intent-reading, like "don't edit code when only asked a question") are frequently violated — the model's "helpfulness" default overrides an inconspicuous rule.

This yields three design countermeasures:

1. **Don't entrust make-or-break matters to "behavioral compliance"; make the "correct action" the "zero-cost default action."**
   → That's why the index lives in AGENTS.md: reading the index isn't an instruction to obey, it's **right there in front of you** — navigation is nearly fail-safe.
2. **Write maintenance rules as concrete "next actions" in the workflow, not abstract slogans.**
   → ❌ "You must keep the index up to date"; ✅ "After creating a wiki file, your **next action** is to append an index row + a log entry." Rules constraining tool actions are far more robust than rules constraining intent-reading.
3. **Acknowledge there will be misses, so Lint is required.** Behavioral instructions will be violated occasionally; Lint periodically scans for drift and repairs it — a hedge against imperfect compliance.

---

## 8. Bootstrap Flow for the AI (how to use this doc)

This document is meant to be read by the AI. In a new project, the AI reads this and then sets up the knowledge base as follows:

1. **Survey**: if there is existing code, read it first; for an empty project, skip the code reading. Then confirm positioning, tech stack, existing architecture and decisions with the user — for an empty project, anything still unclear, use placeholder values to scaffold first and fill in as the project progresses.
2. **Build the base layer**: create `AGENTS.md` in the **project root** (CRITICAL rules + 1-line positioning + index skeleton).
3. **Build the reveal-layer skeleton**: create `log.md` (empty skeleton) + the 4 fixed empty subdirectories under `wiki/`.
4. **Fill an initial architecture**: write at least one `wiki/architecture/overview.md`, and register it in the index.
5. **Self-check**: use the Section 9 checklist.

> Principle: scaffold first, fill knowledge as you go; the index must stay in sync with reality.

---

## 9. Checklist

| Check | Notes |
|---|---|
| AGENTS.md is in the **project root**? | Subdirectory ones aren't auto-loaded |
| CRITICAL maintenance rules at the top of AGENTS.md? | Tool-action-level, prominent |
| Index lives permanently in AGENTS.md, not externalized? | Externalizing self-destructs the premise |
| Index matches the actual wiki? | No missing / ghost entries |
| Only 4 fixed subdirectories + root-level loose under `wiki/`? | Other subdirectories forbidden |
| All 4 fixed directories exist (even as empty skeletons)? | Architectural completeness |
| Every fixed page uses its template? | Structural consistency |
| No raw layer? | This pattern has none |
| Sessions archived on demand, after summarization? | Raw sessions not stored |
| Lint run periodically? | Self-healing net |
| Single source of truth? Same knowledge authoritative in only one place? | Elsewhere only linked |
| AGENTS.md ≤ ~300 lines? | Slimming Lint if exceeded |

---

## 10. Anti-Patterns (collection)

1. **AGENTS.md in the wrong place** (not project root) → not auto-loaded, pattern fails
2. **Index externalized / lazy-loaded** → navigation hub invisible, self-destructs the premise
3. **Creating top-level directories under wiki/** → breaks the fixed structure, finds a place outside the 4 fixed categories
4. **Setting up a raw layer** → this pattern doesn't need one; the material is just wiki content
5. **Archiving raw sessions in full** → unbounded growth and rot; instead archive summarized, on demand
6. **Three-level directory trees** → the AI navigates via index + titles, not folder depth; use flat files + templates
7. **Relying on behavioral instructions, skipping Lint** → behavioral rules will be violated occasionally; Lint is the required self-healing net
8. **Copying the same knowledge in multiple places** → violates single source of truth, inevitably drifts

---

*Version: v1.2 (EN translation; bootstrap adds empty-project branch) | Updated: 2026-06-20*
