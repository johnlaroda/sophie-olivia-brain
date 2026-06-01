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
   - refund/exchange → `#ops-return`
   - policy → `#cs-hub`, `#cs-updates-announcements`
4. Draft a reply in brand voice. If the case needs a refund, ALSO draft a
   `#ops-return` post (order #, issue summary, amount, recommendation).
5. If precedent is unclear or policy is missing, do NOT guess — write a
   "NEEDS JOHN" note at the top of the draft.
6. Write the draft to `ops/drafts/YYYY-MM-DD-ticket-<id>.md` containing:
   the customer reply, any refund-request post, and sources checked.
7. Append a line to today's `logs/` file: ticket id, issue type, what you read/drafted.

## Never
Send the reply, post to Slack, or refund. John does all of that.
