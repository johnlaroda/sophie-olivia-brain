---
name: so-supplier
description: Use when checking Sophie & Olivia orders for fulfillment problems (late, stuck, lost, stock issues). Reads Shopify orders plus supplier context and Slack history, drafts a customer update to ops/drafts/, and STAGES the DayOne supplier message as an unsent Slack draft in #dayone-fulfillment for John to send. Never sends anything itself.
---

# so-supplier — Draft Supplier & Customer Messages (read & draft only)

## Trust
READ & DRAFT ONLY. Never *send* a message to DayOne, never *send* to a customer.
John presses send every time.

**How "draft" works for DayOne (important):** the DayOne channels are **Slack
Connect / externally-shared** channels, so Slack blocks any API from posting into
them — a direct send is impossible by design. The supplier "draft" is therefore
staged as an **unsent Slack draft** via `slack_send_message_draft` into
`#dayone-fulfillment`; it appears in that channel ready for John to review and
send with one click. Staging an unsent draft is NOT a send and is the intended
delivery path here. (If `slack_send_message_draft` ever fails, fall back to
writing the message into the `ops/drafts/` file only.)

## DayOne channels & contacts (verified)
- `#dayone-fulfillment` — **C0ABSSUG0P2** — delay lists, lost/stuck parcels, reships, new tracking. (Slack Connect.)
- `#dayone-orders` — order-specific issues. `#dayone-quality` — defects. `#dayone-products` — range questions. (All Slack Connect.)
- Tag both contacts: **Catherine** `<@U07QG6PTFC4>` and **Shirley** `<@U0B6FPDRKPH>`. Do NOT tag Alina (left DayOne).
- House format observed in-channel: tag Catherine + Shirley, order #, **full ship-to address**, then "let me know if you'll generate a new tracking — thanks!"

## Inputs
- Optional: a specific order #. Otherwise scan recent orders for problems.

## Steps
1. Read `context/suppliers.md` and `context/brand-voice.md`.
2. Via Shopify MCP, find orders that are late/stuck/unfulfilled/lost past the SLA in
   `context/suppliers.md` (or the order # given). For a reship, also pull the order's
   **line items (title + SKU + qty)** and the **shipping address** — DayOne needs both.
3. Search `#dayone-fulfillment` (delays/reships) and `#dayone-orders` (order-specific),
   plus `#dayone-quality` if a defect, for prior handling of the same batch/issue.
   Don't duplicate an open thread.
4. Compose the DayOne message in the house format above (tag Catherine + Shirley,
   order #, SKU, full ship-to address, specific ask, e.g. "generate new tracking and reship").
5. Compose a customer update in brand voice (honest, no over-promising on dates we
   don't control).
6. **Stage** the DayOne message as an unsent Slack draft via `slack_send_message_draft`
   to channel **C0ABSSUG0P2** (`#dayone-fulfillment`). Record the returned `draft_id`.
7. Write BOTH messages (supplier + customer) to `ops/drafts/YYYY-MM-DD-order-<id>.md`
   with sources checked and the Slack `draft_id`, so there's a file record too.
8. Append a line to today's `logs/` file: order id, problem, what you drafted/staged.

## Never
Send the DayOne message (John clicks send on the staged Slack draft), send the
customer reply, or issue a refund. If a reship can't be done (stock/logistics),
flag it for John for a refund decision (#ops-return) — never auto-refund.
