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
5. Auto-DM the finished report to John's own Slack DM (self only — the one permitted send; see CLAUDE.md).
6. Append a line to today's `logs/` file: report type + headline.

## Never
Write to Shopify, or send to anyone other than John's own Slack DM. No customer, supplier, or channel sends.
