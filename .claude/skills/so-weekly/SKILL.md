---
name: so-weekly
description: Use for a Monday Sophie & Olivia business review. Pulls the week's Shopify numbers, scores them against the Q2 targets, writes a review to ops/reports/, and auto-DMs it to John. Read only otherwise.
---

# so-weekly — Weekly Q2 Scorecard (read only)

## Trust
READ ONLY. Write the report and auto-DM it to John's own Slack DM (the only permitted send).

## Inputs
- Default: last 7 days vs the prior 7 days.

## Steps
1. Read context/business.md for the Q2 target scorecard (all AUD).
2. Via Shopify analytics, pull for the week: revenue, orders, AOV, conversion rate, return
   rate, fulfillment time, late-order count. Compare to the prior week AND to the Q2 targets.
3. Write to ops/reports/YYYY-MM-DD-weekly.md:
   - headline (on-track / off-track vs targets)
   - a scorecard table: metric | target | this week | trend vs last week
   - 2-3 priorities for the week (tie them to the 5 goals in business.md)
4. Auto-DM the finished report to John's own Slack DM (self only). Append a line to today's logs/ file.

## Never
Write to Shopify, or send to anyone other than John's own Slack DM.
