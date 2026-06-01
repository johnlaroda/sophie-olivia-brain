---
name: so-morning-briefing
description: Use each morning for John's Sophie & Olivia briefing. Bundles the daily sales snapshot with a stuck-order / refund / quality ticket scan, then DMs John the snapshot plus a "needs your decision" list. Read-only + draft-and-ask — never sends to customers/suppliers or issues refunds on its own.
---

# so-morning-briefing — Daily Briefing + Decision List (read-only, draft-and-ask)

## Trust
READ-ONLY on the business + DRAFT-AND-ASK. The ONLY thing this sends unprompted is
the briefing itself, to **John's own Slack DM** (the approved self-DM exception in
CLAUDE.md). It NEVER sends a customer reply, supplier message, or refund on its own.
For anything actionable it presents the draft and waits for John's "go".

## Inputs
- None (defaults to yesterday for sales; recent open items for scans).

## Steps
1. Read context/business.md (Q2 targets, AUD), context/suppliers.md (SLAs/flag
   thresholds), context/policies.md.
2. **Sales snapshot** — run the so-report logic for "daily" (yesterday): revenue,
   orders, AOV, refund rate, late/unfulfilled count, vs prior day. All AUD.
3. **Stuck-order scan** — via Shopify, find orders past the DayOne SLA / flag
   thresholds in suppliers.md (Pending >2 business days, Info Received >3 days,
   In Transit >13 days). List the worst few. Do NOT draft full messages yet.
4. **Ticket scan** — via Gorgias, surface open refund/quality tickets needing a
   decision (e.g. refund amount pending, defect to report). List them.
5. **Compose the briefing** and DM it to John's own Slack DM. Format:
   > 📊 Morning briefing — <date>
   > Sales A$X (+/-Y% DoD), return rate Z% (target 1.2%).
   > ⚠️ N items need your decision:
   > • Order #__ — stuck N days. Reply "go" and I'll draft the DayOne + customer msgs (so-supplier).
   > • Ticket #__ — refund/credit pending your amount (so-refund).
   > • Quality ticket #__ — reply "go" to draft the #dayone-quality report (so-quality).
   > • Sizing returns trending — want the full so-sizing-watch?
6. **Wait for John.** When John replies "go" / "skip" / "change X" for an item,
   hand off to the matching skill (so-supplier / so-refund / so-quality /
   so-sizing-watch) which DRAFTS to ops/drafts/ — still never sending.
7. Append a line to today's logs/ file: "so-morning-briefing — <headline>, N decisions flagged".

## Never
Send any customer reply, supplier message, or refund. The only autonomous send is
the briefing to John's own Slack DM. Everything actionable is draft-and-ask.
