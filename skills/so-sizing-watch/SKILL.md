---
name: so-sizing-watch
description: Use to quantify how much of Sophie & Olivia's returns and tickets are driven by the "runs ~2 sizes small" issue. Reads Gorgias + Shopify, writes an analysis to ops/reports/, and auto-DMs it to John. Read only otherwise.
---

# so-sizing-watch — Quantify Sizing-Driven Returns (read only)

## Trust
READ ONLY. Analyse and write a report file. Change nothing. The only permitted send is
auto-DMing the finished report to John's own Slack DM (see CLAUDE.md).

## Inputs
- Period: default last 30 days.

## Steps
1. Read context/products.md (the sizing issue) and context/business.md (return-rate target 1.2%).
2. Via Gorgias, pull recent support tickets and classify how many are sizing/fit-related
   ("too small", "too tight", "size up", "doesn't fit", band/cup, etc.).
3. Via Shopify, pull returns/refunds for the period; estimate how many are sizing-driven.
4. Compute: total returns, sizing-driven count and %, the share of CS volume that is sizing,
   and the rough A$ cost (refunds + return shipping where it's ours). All figures in AUD.
5. Write to ops/reports/YYYY-MM-DD-sizing-watch.md:
   - headline (e.g. "Sizing drove ~X% of returns this month, ~A$Y")
   - the numbers
   - top offending SKUs / lines if visible
   - 1-3 recommendations (size-chart fixes, product-page warnings, supplier pressure)
6. Auto-DM the finished report to John's own Slack DM (self only). Append a line to today's logs/ file.

## Never
Write to Shopify/Gorgias, or send to anyone other than John's own DM.
