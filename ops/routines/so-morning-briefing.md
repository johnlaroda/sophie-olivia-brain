# Routine Spec — `so-morning-briefing`

**Status:** Approved shape (John, 2026-06-01). NOT yet live — requires the setup
in the "Going live" section below (GitHub repo + claude.ai connectors).

## Summary
A scheduled remote routine that wakes up each weekday morning, does the reading,
and hands John a tidy briefing + decision list. **Draft-and-ask only — it never
sends to customers/suppliers or issues refunds on its own.**

## Config
| Field | Value |
|---|---|
| Name | `so-morning-briefing` |
| Trigger | Schedule — every weekday 7:00am Asia/Manila (cron `0 23 * * 0-4` UTC) |
| Runs | `so-report` (daily) + a quick late-order / ticket scan |
| Trust | Read-only analysis + draft-and-ask. Zero autonomous external sends. |

## What it does each run
1. Pull yesterday's Shopify numbers → build the daily snapshot (AUD).
2. Scan for stuck orders (past DayOne SLA) and refund/quality tickets needing attention.
3. DM John the snapshot **plus a short "needs your call" list**, e.g.:
   > 📊 Morning briefing — <date>
   > Sales A$X (+Y%), return rate Z% (vs 1.2% target).
   > ⚠️ N items need your decision:
   > • Order #____ — stuck N days. Draft supplier msg ready — reply "go" to prep it.
   > • Ticket #____ — refund/credit pending your amount.
   > • Sizing returns trending — want the full so-sizing-watch?

## Guardrails (the human-in-the-loop John asked for)
- **Informs and drafts only.** Never sends a customer reply, supplier message,
  or refund autonomously.
- For anything actionable, it **presents the draft and waits for John's reply**
  ("go" / "skip" / "change X"). John always pulls the trigger.
- The only unprompted send is the briefing itself — to **John's own DM** (the
  already-approved self-DM exception in CLAUDE.md).

## Going live (prerequisites — Option A setup)
1. **Push `Brain` to a private GitHub repo** so the routine can clone the skills +
   context. (Remote agents cannot see local files.)
2. **Connect Shopify, Gorgias, and Slack** at https://claude.ai/customize/connectors
   so the routine has live data + can DM John.
3. **Adjust output destination:** remote runs can't write to local `ops/`. The
   briefing goes to John's Slack DM; any drafts John approves get prepared in the
   reply thread (or written back to the repo), not the local machine.
4. Create the routine via the schedule tooling with the cron above, then test with
   a manual "run now" before trusting the schedule.

## Future graduations (after trust)
- Add a Monday `so-weekly` routine.
- Add a weekly `so-sizing-watch` routine.
- Webhook trigger: run a triage when a new high-priority Gorgias ticket arrives.
