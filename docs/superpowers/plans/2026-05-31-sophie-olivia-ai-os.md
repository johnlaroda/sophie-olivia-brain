# Sophie & Olivia AI OS Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Stand up a file-based AI Operating System for the Sophie & Olivia Shopify lingerie business in Claude Code, at trust level "A" (read & draft only).

**Architecture:** A `Brain` folder holds stable knowledge as markdown (`context/`), a session-orienting `CLAUDE.md`, a working area for drafts/reports (`ops/`), an audit trail (`logs/`), and three Claude Code skills (`so-support`, `so-supplier`, `so-report`) that read knowledge files + live MCP data (Shopify/Gorgias/Slack) and produce drafts only. Nothing sends autonomously.

**Tech Stack:** Markdown knowledge files; Claude Code skills (SKILL.md); MCP connectors (Shopify, Gorgias, Slack, Notion). No build system, no test runner — verification is done by running Claude against a real case and confirming behavior.

**Note on "tests":** This is a knowledge/skill build, not application code. Each task's verification step is a manual check (does the file exist with the right sections / does Claude behave correctly), not an automated test.

**Spec:** `docs/superpowers/specs/2026-05-31-sophie-olivia-ai-os-design.md`

---

## File Structure

Files created by this plan (all under `C:\Users\HOME\Documents\Brain\`):

- `CLAUDE.md` — session orientation; tells Claude who John is, the trust level, and where knowledge lives.
- `context/business.md` — S&O overview, goals, key numbers, key people.
- `context/brand-voice.md` — customer-reply tone and do/don't list.
- `context/products.md` — product lines, sizing/fit notes, common fit complaints.
- `context/policies.md` — refund/exchange rules + John's precedents.
- `context/suppliers.md` — DayOne contacts, SLAs, escalation path.
- `ops/drafts/.gitkeep`, `ops/reports/.gitkeep`, `logs/.gitkeep` — working dirs.
- `skills/so-support/SKILL.md` — refine existing CS skill into draft-only flow.
- `skills/so-supplier/SKILL.md` — supplier ops draft flow.
- `skills/so-report/SKILL.md` — BI snapshot flow.

---

## Task 1: Initialize the Brain as a git repo

**Files:**
- Create: `.gitignore`

- [ ] **Step 1: Initialize git**

Run:
```bash
git init
```
Expected: "Initialized empty Git repository in C:/Users/HOME/Documents/Brain/.git/"

- [ ] **Step 2: Create `.gitignore`**

Create `.gitignore` with:
```
# OS noise
Thumbs.db
.DS_Store

# Drafts and reports are working artifacts, not source — keep dirs, ignore contents
ops/drafts/*
ops/reports/*
logs/*
!ops/drafts/.gitkeep
!ops/reports/.gitkeep
!logs/.gitkeep
```

- [ ] **Step 3: Verify**

Run:
```bash
git status
```
Expected: shows `.gitignore` and the existing `docs/` spec+plan as untracked.

- [ ] **Step 4: Commit**

```bash
git add .gitignore docs/
git commit -m "chore: init Brain repo with spec and plan"
```

---

## Task 2: Create the working directories

**Files:**
- Create: `ops/drafts/.gitkeep`
- Create: `ops/reports/.gitkeep`
- Create: `logs/.gitkeep`

- [ ] **Step 1: Create the three .gitkeep files**

Create each file with a single comment line, e.g. `ops/drafts/.gitkeep`:
```
# Drafted customer replies and refund posts await John's approval here.
```
`ops/reports/.gitkeep`:
```
# Saved BI snapshots (daily/weekly) live here.
```
`logs/.gitkeep`:
```
# Per-session audit trail of what Claude read and drafted.
```

- [ ] **Step 2: Verify**

Run:
```bash
git status
```
Expected: the three `.gitkeep` files appear as untracked.

- [ ] **Step 3: Commit**

```bash
git add ops/ logs/
git commit -m "chore: add ops/drafts, ops/reports, logs working dirs"
```

---

## Task 3: Write context/business.md

**Files:**
- Create: `context/business.md`

- [ ] **Step 1: Write the file**

Create `context/business.md`. Replace bracketed prompts with John's real info; leave a clearly-marked `> FILL:` note where John must supply data later rather than inventing it.

```markdown
# Sophie & Olivia — Business Overview

## What we are
Online intimate lingerie brand. Platform: Shopify. Fulfilled via supplier "DayOne".

## Goals (current)
> FILL: John's top 1-3 goals for this quarter (e.g. revenue target, reduce refund rate, cut shipping delays).

## Key numbers
> FILL: typical monthly orders, AOV, current refund rate, top 3 SKUs. (Claude can also pull these live from Shopify.)

## Key people
- John — owner / CS manager. Approves all refunds (via Slack `#cs-refundrequest`).
- DayOne — supplier (orders, stock, quality). See `context/suppliers.md`.

## Tools
- Shopify (store + orders + analytics) — via MCP
- Gorgias (support tickets) — via MCP
- Slack (internal coordination + supplier channels) — via MCP
- Notion (docs) — via MCP

## How we work (trust level)
Claude operates READ & DRAFT ONLY. It never sends customer messages, posts to
Slack, or issues refunds on its own. John reviews and sends everything.
```

- [ ] **Step 2: Verify**

Confirm the file has sections: What we are, Goals, Key numbers, Key people, Tools, How we work. Confirm `> FILL:` markers are present where real data is needed.

- [ ] **Step 3: Commit**

```bash
git add context/business.md
git commit -m "docs: add business overview context"
```

---

## Task 4: Write context/brand-voice.md

**Files:**
- Create: `context/brand-voice.md`

- [ ] **Step 1: Write the file**

Create `context/brand-voice.md`:
```markdown
# Brand Voice — Customer Replies

## Tone
Warm, reassuring, discreet, professional. We sell intimate apparel — always
treat sizing/fit/body topics with sensitivity and zero judgment.

## Always
- Address the customer by first name.
- Acknowledge the feeling before the fix ("I'm sorry the fit wasn't right…").
- Be concrete: order number, next step, timeframe.
- Offer the easiest path to resolution that policy allows.

## Never
- Clinical, blunt, or embarrassing language about the body.
- Over-promising on dates we can't control (DayOne shipping).
- Making up policy — if unsure, draft flags it for John.

## Sign-off
> FILL: standard sign-off (e.g. "Warmly, the Sophie & Olivia team").
```

- [ ] **Step 2: Verify**

Confirm Tone / Always / Never / Sign-off sections exist.

- [ ] **Step 3: Commit**

```bash
git add context/brand-voice.md
git commit -m "docs: add brand voice context"
```

---

## Task 5: Write context/products.md

**Files:**
- Create: `context/products.md`

- [ ] **Step 1: Write the file**

Create `context/products.md`:
```markdown
# Products — Sizing & Fit Notes

## Lines
> FILL: list main product lines/collections. (Claude can also pull live from Shopify.)

## Sizing guidance
> FILL: how S&O sizing runs (true to size / small / large), the size chart link,
> band/cup conversion notes.

## Common fit complaints & standard answers
> FILL: the 3-5 fit issues that recur (e.g. "band too tight", "cup gaping") and
> the answer/remedy John gives for each. Used to draft accurate support replies.
```

- [ ] **Step 2: Verify**

Confirm Lines / Sizing guidance / Common fit complaints sections exist.

- [ ] **Step 3: Commit**

```bash
git add context/products.md
git commit -m "docs: add product & sizing context"
```

---

## Task 6: Write context/policies.md

**Files:**
- Create: `context/policies.md`

- [ ] **Step 1: Write the file**

Create `context/policies.md`:
```markdown
# Policies — Refunds, Exchanges, Precedents

## Refunds
- All refunds require John's approval via Slack `#cs-refundrequest`.
- Claude DRAFTS the refund-request post; it never issues a refund.
> FILL: standard refund window (e.g. 30 days), hygiene/intimate-apparel return
> restrictions, who pays return shipping.

## Exchanges
> FILL: exchange window and process (especially size swaps).

## Precedents (John's past decisions)
> FILL / GROW OVER TIME: notable rulings to keep replies consistent.
> Claude should also search `#cs-refundrequest` for live precedent.

## Escalation
- Unclear precedent → draft a note for John (do not guess).
- Quality defect → also document in Slack `#dayone-quality` (drafted, John posts).
```

- [ ] **Step 2: Verify**

Confirm Refunds / Exchanges / Precedents / Escalation sections exist and that the "requires John's approval / never issues a refund" rule is stated.

- [ ] **Step 3: Commit**

```bash
git add context/policies.md
git commit -m "docs: add refund/exchange policy context"
```

---

## Task 7: Write context/suppliers.md

**Files:**
- Create: `context/suppliers.md`

- [ ] **Step 1: Write the file**

Create `context/suppliers.md`:
```markdown
# Suppliers — DayOne

## Contacts
> FILL: primary contact name + channel (Slack `#dayone-*` / email).

## Channels
- `#dayone-general` — general questions/policies
- `#dayone-orders` — fulfillment, shipping, stock issues
- `#dayone-quality` — defects, material/quality issues

## SLAs / expectations
> FILL: typical fulfillment time, restock lead time, how late is "late".

## Escalation path
> FILL: when/how to escalate a stuck order or a quality batch.

## Message style
Professional, specific: always include order #, SKU, and the exact issue.
```

- [ ] **Step 2: Verify**

Confirm Contacts / Channels / SLAs / Escalation / Message style sections exist.

- [ ] **Step 3: Commit**

```bash
git add context/suppliers.md
git commit -m "docs: add supplier (DayOne) context"
```

---

## Task 8: Write CLAUDE.md (session orientation)

**Files:**
- Create: `CLAUDE.md`

- [ ] **Step 1: Write the file**

Create `CLAUDE.md`:
```markdown
# Sophie & Olivia — AI Operating System

You are John's operating system for running Sophie & Olivia, a Shopify intimate
lingerie business. This file orients you every session.

## Trust level: A — READ & DRAFT ONLY
- You may READ from Shopify, Gorgias, Slack, Notion (via MCP) and the files below.
- You may DRAFT replies, refund posts, supplier messages, and reports.
- You may NOT send/post/refund/tag autonomously. John presses send every time.
- When in doubt, draft and flag for John. Never invent policy or precedent.

## Where knowledge lives (read these before acting)
- `context/business.md` — overview, goals, numbers, people
- `context/brand-voice.md` — how customer replies should sound
- `context/products.md` — sizing/fit knowledge
- `context/policies.md` — refund/exchange rules + precedents
- `context/suppliers.md` — DayOne contacts, channels, SLAs

## Where you write
- Drafts (customer replies, refund posts, supplier msgs) → `ops/drafts/`
- BI snapshots → `ops/reports/`
- After each session, append what you read + drafted to a dated file in `logs/`.

## Skills
- `so-support` — draft a reply for a Gorgias ticket.
- `so-supplier` — draft supplier + customer messages for late/stuck orders.
- `so-report` — draft a sales/BI snapshot from Shopify analytics.
```

- [ ] **Step 2: Verify**

Confirm the trust-level rules, the five context-file pointers, the write locations, and the three skills are all listed.

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: add CLAUDE.md session orientation"
```

---

## Task 9: Build skills/so-support/SKILL.md

**Files:**
- Create: `skills/so-support/SKILL.md`
- Reference: existing `sophie--olivia-brand` skill (reuse its Slack-channel routing knowledge)

- [ ] **Step 1: Write the skill**

Create `skills/so-support/SKILL.md`:
```markdown
---
name: so-support
description: Use when handling a Sophie & Olivia customer support ticket. Reads the Gorgias ticket plus knowledge files and Slack precedent, then DRAFTS a reply (and a refund-request post if needed) to ops/drafts/. Never sends.
---

# so-support — Draft a Support Reply (read & draft only)

## Trust
READ & DRAFT ONLY. Never send a Gorgias reply, never post to Slack, never issue
a refund. Output is a draft file for John to review and send.

## Inputs
- A Gorgias ticket (id or selected ticket).

## Steps
1. Read `context/brand-voice.md`, `context/policies.md`, `context/products.md`.
2. Fetch the ticket via Gorgias MCP. Identify issue type: order/shipping,
   product/fit, refund/exchange, or policy question.
3. Search Slack for precedent using the routing below. Use SPECIFIC keywords
   (order #, SKU, issue). Check recent messages first, widen if needed:
   - order/shipping → `#dayone-orders`
   - product/quality → `#dayone-quality`
   - refund/exchange → `#cs-refundrequest`
   - policy → `#cs-hub`, `#cs-updates-announcements`
4. Draft a reply in brand voice. If the case needs a refund, ALSO draft a
   `#cs-refundrequest` post (order #, issue summary, amount, recommendation).
5. If precedent is unclear or policy is missing, do NOT guess — write a
   "NEEDS JOHN" note at the top of the draft.
6. Write the draft to `ops/drafts/YYYY-MM-DD-ticket-<id>.md` containing:
   the customer reply, any refund-request post, and sources checked.
7. Append a line to today's `logs/` file: ticket id, issue type, what you read/drafted.

## Never
Send the reply, post to Slack, or refund. John does all of that.
```

- [ ] **Step 2: Verify (real-case dry run)**

Pick a real low-stakes Gorgias ticket. Invoke `so-support` on it. Confirm:
- It read the three context files (visible in its actions).
- It produced `ops/drafts/…-ticket-<id>.md` with a reply.
- It did NOT send anything in Gorgias/Slack.
Expected: a send-ready draft file, nothing sent.

- [ ] **Step 3: Commit**

```bash
git add skills/so-support/SKILL.md
git commit -m "feat: add so-support draft-only skill"
```

---

## Task 10: Build skills/so-supplier/SKILL.md

**Files:**
- Create: `skills/so-supplier/SKILL.md`

- [ ] **Step 1: Write the skill**

Create `skills/so-supplier/SKILL.md`:
```markdown
---
name: so-supplier
description: Use when checking Sophie & Olivia orders for fulfillment problems (late, stuck, stock issues). Reads Shopify orders plus supplier context and Slack history, then DRAFTS a supplier message and a customer update to ops/drafts/. Never sends.
---

# so-supplier — Draft Supplier & Customer Messages (read & draft only)

## Trust
READ & DRAFT ONLY. Never message DayOne, never post to Slack, never email a
customer. Output is draft files for John.

## Inputs
- Optional: a specific order #. Otherwise scan recent orders for problems.

## Steps
1. Read `context/suppliers.md` and `context/brand-voice.md`.
2. Via Shopify MCP, find orders that are late/stuck/unfulfilled past the SLA in
   `context/suppliers.md` (or the order # given).
3. For each, search `#dayone-orders` (and `#dayone-quality` if a defect) for
   prior handling of the same batch/issue. Don't duplicate an open thread.
4. Draft a supplier message (order #, SKU, expected vs actual, specific ask) in
   the professional style from `context/suppliers.md`.
5. Draft a customer update in brand voice (honest, no over-promising on dates).
6. Write both to `ops/drafts/YYYY-MM-DD-order-<id>.md` with sources checked.
7. Append a line to today's `logs/` file: order id, problem, what you drafted.

## Never
Send to DayOne, post to Slack, or message the customer. John sends.
```

- [ ] **Step 2: Verify (real-case dry run)**

Run `so-supplier` (let it scan, or give it a known late order). Confirm:
- It read `suppliers.md` + `brand-voice.md`.
- It produced `ops/drafts/…-order-<id>.md` with both a supplier message and a customer update.
- Nothing was sent/posted.
Expected: two send-ready drafts in one file, nothing sent.

- [ ] **Step 3: Commit**

```bash
git add skills/so-supplier/SKILL.md
git commit -m "feat: add so-supplier draft-only skill"
```

---

## Task 11: Build skills/so-report/SKILL.md

**Files:**
- Create: `skills/so-report/SKILL.md`

- [ ] **Step 1: Write the skill**

Create `skills/so-report/SKILL.md`:
```markdown
---
name: so-report
description: Use when John wants a Sophie & Olivia sales/BI snapshot. Pulls Shopify analytics, compares to the prior period, and writes a plain-English report to ops/reports/. Read only.
---

# so-report — Draft a BI Snapshot (read only)

## Trust
READ ONLY. Pull analytics and write a report file. Change nothing in Shopify.

## Inputs
- Period: "daily" (default = yesterday) or "weekly" (last 7 days vs prior 7).

## Steps
1. Read `context/business.md` for goals/key numbers to frame the report.
2. Via Shopify MCP (ShopifyQL / analytics), pull for the period:
   - revenue, order count, AOV
   - top sellers (units + revenue)
   - refund rate / refund count
   - late or unfulfilled orders count
3. Compute change vs the prior comparable period.
4. Write a plain-English snapshot to `ops/reports/YYYY-MM-DD-<daily|weekly>.md`:
   - one-line headline (e.g. "Revenue up 8% WoW, refunds steady")
   - the numbers with deltas
   - 1-3 things worth John's attention
5. Append a line to today's `logs/` file: report type + headline.

## Never
Write to Shopify or take any action. This is reporting only.
```

- [ ] **Step 2: Verify (real-case dry run)**

Run `so-report` for "daily". Confirm:
- It read `business.md`.
- It pulled real Shopify numbers and wrote `ops/reports/…-daily.md` with a headline, numbers + deltas, and attention items.
- It changed nothing in Shopify.
Expected: a readable snapshot file.

- [ ] **Step 3: Commit**

```bash
git add skills/so-report/SKILL.md
git commit -m "feat: add so-report read-only BI skill"
```

---

## Task 12: Fill in the `> FILL:` knowledge gaps (John-supplied)

**Files:**
- Modify: `context/business.md`, `context/brand-voice.md`, `context/products.md`, `context/policies.md`, `context/suppliers.md`

- [ ] **Step 1: Walk John through each `> FILL:` marker**

Go file by file. For each `> FILL:` prompt, ask John for the real value and
replace the marker. Where Shopify can supply it live (numbers, SKUs), note that
and leave the file pointing at the live source instead of hardcoding stale data.

- [ ] **Step 2: Verify**

Search all `context/*.md` for remaining `> FILL:` markers.
Run:
```bash
git grep "FILL:" context/
```
Expected: only the deliberately-live ones remain (each with a note explaining why).

- [ ] **Step 3: Commit**

```bash
git add context/
git commit -m "docs: fill in S&O knowledge from John"
```

---

## Task 13: End-to-end shakedown

- [ ] **Step 1: Fresh-session check**

Start a fresh Claude session in `Brain`. Without extra prompting, confirm Claude
picks up `CLAUDE.md`, knows the trust level, and knows where context lives.

- [ ] **Step 2: Run all three skills once on real cases**

Run `so-support`, `so-supplier`, and `so-report` on real low-stakes cases.
Confirm each: read the right context files, produced a draft/report, sent nothing,
and logged to `logs/`.

- [ ] **Step 3: Confirm the guardrail held**

Verify nothing was sent/posted/refunded in Gorgias, Slack, or Shopify during any run.
Expected: all output is files in `ops/` + `logs/`; source tools untouched.

- [ ] **Step 4: Commit any fixes**

```bash
git add -A
git commit -m "chore: end-to-end shakedown fixes"
```

---

## Deferred (not in this plan — future, after trust earned)

- **Cadence:** schedule `so-report` to run each morning once it's proven reliable by hand.
- **Trust level B:** let `so-support` auto-tag tickets / post internal notes.
- **Marketing/content** skills.
- **Team access** beyond John.
