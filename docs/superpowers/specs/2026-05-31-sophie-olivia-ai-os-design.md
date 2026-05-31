# Sophie & Olivia — AI Operating System (Design Spec)

**Date:** 2026-05-31
**Owner:** John
**Status:** Approved — ready for implementation planning

## Purpose

Build a personalized AI Operating System for Sophie & Olivia (a Shopify intimate
lingerie business) inside Claude Code, following the "Four C's" framework
(Context, Connections, Capabilities, Cadence) and the "Bike Method" for agent
trust. The goal is to give John back time on the three heaviest daily workloads:
**customer support**, **supplier operations**, and **business intelligence**.

Marketing/content is explicitly **out of scope** for v1 (YAGNI — add later once
the core works).

## Users & Trust Level

- **Single user:** John. The CS team continues using Gorgias/Shopify directly for now.
- **Trust level (Bike Method): "A" — read & draft only.** Claude reads from
  Shopify/Gorgias/Slack and *drafts* replies, refund posts, supplier messages,
  and reports. **John presses send/approve every time. Nothing acts autonomously.**

## The Four C's — Current State

| C | Status | Notes |
|---|--------|-------|
| **Context** | Partial | Some knowledge in the existing CS skill + scattered in Slack. Needs consolidation into files. |
| **Connections** | ✅ Done | Shopify, Gorgias, Slack, Notion already wired via MCP. |
| **Capabilities** | Minimal | One CS skill exists. Build/refine three skills. |
| **Cadence** | None | Deferred until trust earned (Bike Method). |

**Principle:** Stable knowledge lives in **files**; live data is pulled fresh
from **MCP** (Shopify/Gorgias/Slack) each session.

## Architecture — Folder Layout

```
C:\Users\HOME\Documents\Brain\
├── CLAUDE.md                  # Loaded every session: who John is, how S&O works, where things live
├── context/                   # STABLE KNOWLEDGE (John maintains; the competitive edge)
│   ├── business.md            # S&O overview, goals, key numbers, who's who (John, DayOne)
│   ├── brand-voice.md         # Tone for customer replies (discreet, warm, professional)
│   ├── products.md            # Product lines, sizing/fit notes, common fit complaints
│   ├── policies.md            # Refund rules, exchange rules, John's precedents
│   └── suppliers.md           # DayOne contacts, SLAs, escalation path
├── skills/                    # CAPABILITIES (3 skills below)
├── ops/                       # Working area Claude writes to
│   ├── drafts/                # Drafted replies / refund posts awaiting approval
│   └── reports/               # Saved BI snapshots
└── logs/                      # Per-session record of what Claude did (audit/trust trail)
```

## Components — The Three Skills

All three operate at trust level **A (read & draft only)**.

### 1. `so-support` (refine existing `sophie--olivia-brand` skill)
- **Input:** a Gorgias ticket.
- **Process:** search Slack precedents (`#cs-hub`, `#ops-return`,
  `#dayone-*`) + `context/policies.md` + `context/brand-voice.md`.
- **Output:** a drafted reply written to `ops/drafts/`. Refund cases produce a
  drafted `#ops-return` post for John to send.
- **Never sends.** No customer-facing or refund action is taken autonomously.

### 2. `so-supplier` (new)
- **Input:** Shopify order data (late/stuck orders, stock issues).
- **Process:** check `#dayone-orders` / `#dayone-quality` for prior handling +
  `context/suppliers.md`.
- **Output:** a drafted supplier message + a drafted customer update, both to
  `ops/drafts/`. **John sends.**

### 3. `so-report` (new)
- **Input:** Shopify analytics (ShopifyQL).
- **Process:** pull sales/orders/refunds; compare to prior period.
- **Output:** a plain-English daily/weekly snapshot (top sellers, refund rate,
  late orders, revenue vs last week) to `ops/reports/`.

## Data Flow

1. John asks Claude to handle a ticket / check orders / run a report.
2. Claude reads stable knowledge from `context/` files (loaded via `CLAUDE.md`).
3. Claude pulls live data via MCP (Gorgias / Shopify / Slack).
4. Claude produces a **draft** (file in `ops/drafts/` or `ops/reports/`).
5. John reviews and sends/approves manually in the source tool.
6. Claude appends a line to `logs/` recording what it read and drafted.

## Guardrails (Bike Method)

- **Default = read + draft.** John presses send in Gorgias/Slack/Shopify.
- **No autonomous customer-facing or refund actions.** Ever, at level A.
- **Every session logs** what it touched to `logs/` — builds the track record
  needed before graduating any single task to autopilot.
- **Cadence is deferred.** Only after a task (e.g. the daily report) has been
  watched running clean by hand several times do we schedule it. Promote one
  task at a time.

## Out of Scope (v1)

- Marketing/content generation.
- Multi-user / CS-team access.
- Any autonomous (level B/C) writes or sends.
- Automated/scheduled runs (cadence).

## Success Criteria

- The `context/` files capture S&O's stable knowledge well enough that drafts
  are usable with minimal editing.
- Each of the three skills produces a correct, send-ready draft from a real case.
- Nothing is ever sent without John's explicit action.
- `logs/` gives John a clear record to judge when a task is ready to graduate.
