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
