# Sophie & Olivia — Business Overview

## What we are
Online intimate lingerie brand. Platform: Shopify. Fulfilled via supplier "DayOne".

## Currency (canonical)
**All figures are in AUD (A$).** The store transacts and reports in AUD on
Shopify, so AUD is our single source of truth — the `so-report` skill compares
live AUD sales against the AUD targets below.

> ASSUMPTION TO CONFIRM (John): the Q2 targets were originally shown with a `€`
> symbol. We treat those figures as **AUD** (most likely a spreadsheet display
> artifact, since the store operates in AUD). If they were genuinely EUR, convert
> them to AUD at the current rate and update the numbers below.

## Goals (current)
1. Increase revenue (Q2 target A$1,750,000).
2. Cut refund/return rate (target 1.2%; currently ~1.5%).
3. Fix shipping delays (fulfillment target 1.5 days; currently ~2.01 days).
4. Fix quality issues (agreed defect-rate cap with DayOne: 1.5% per batch).
5. Fix sizing issue (garments run ~2 sizes small — see context/products.md).

## Key numbers (Q2 targets vs actuals)
| Metric | Target | Actual |
|---|---|---|
| Revenue | A$1,750,000 | — |
| Conversion rate | 1% | 0.76% |
| Average order value (AOV) | A$82.50 | — |
| Customer satisfaction (CSAT) | 4.4 | 4.27 |
| Resolution time | 2 days | 3.25 days |
| First response time | 2 hours | 0.63 days |
| Return rate | 1.2% | 1.5% |
| Supplier lead time | 10 days | 12.95 days |
| Order fulfillment time | 1.5 days | 2.01 days |
| Customer acquisition cost (CAC) | A$42 | — |
| ROAS | 1.95 | — |

> Live sales figures (revenue, orders, AOV) can be pulled fresh from Shopify via the so-report skill — all in AUD, matching the targets above.

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
