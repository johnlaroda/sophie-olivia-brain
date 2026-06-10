# Suppliers — DayOne

## Contacts (verified Slack IDs)
- **Catherine** — primary POC, always include. Slack: `<@U07QG6PTFC4>` (`@Catherine Dayone`).
- **Shirley** — replaced Alina; tag going forward. Slack: `<@U0B6FPDRKPH>` (`@Shirley Dayone`).
- (Alina is no longer at DayOne — do not tag.)

## Channels
> ⚠️ **All `#dayone-*` channels are Slack Connect (externally shared with DayOne).**
> APIs/bots **cannot post** into them — a direct send fails with
> `mcp_externally_shared_channel_restricted`. To "send" a supplier message, stage an
> **unsent draft** with `slack_send_message_draft`; it appears in the channel for John
> to review and send with one click. (This is fully compatible with draft-and-ask.)

- `#dayone-general` — general questions/policies
- `#dayone-fulfillment` — **C0ABSSUG0P2** — fulfillment status, delay lists, lost/stuck parcels, reships, new tracking
- `#dayone-orders` — order-specific issues
- `#dayone-quality` — defects, material/quality issues
- `#dayone-products` — product/range questions

**House format in `#dayone-fulfillment`** (match it): tag Catherine + Shirley, the
order #, the **full ship-to address**, then "let me know if you'll generate a new
tracking — thanks!"

## SLAs / expectations
- DayOne's stated normal order-to-dispatch time: **~5 days** (≥3 days to reach
  their warehouse + 1–2 days QC/pack/dispatch).
- S&O targets: **fulfillment 1.5 days**, **supplier lead time 10 days**
  (current actuals ~2.01 and ~12.95 days — both over target).
- Agreed **defect-rate cap: 1.5% per batch**.
- "Late" / flag thresholds used by the team:
  - Pending (not dispatched) **> 2 business days** → flag before the customer contacts us
  - Info Received (tracking, no movement) **> 3 days** → flag
  - In Transit **> 13 days** → flag
  - DayOne compensation only applies if undelivered **> 30 days** post-dispatch.

## Escalation path
- Send consolidated delay lists in `#dayone-fulfillment`, tagging Catherine and Shirley
  (link the fulfillment sheet).
- Once CS provides reasonable proof (photos, tracking showing no movement, delivery
  mismatch), the case is validated — no further internal debate needed.
- Reship should be triggered within **24–48 hours** once responsibility is clear; if
  reship can't be done immediately (stock/logistics), a refund should be processed
  promptly rather than held "pending investigation".
- Reference standard: DayOne End-to-End Quality & Fulfillment Standards (Notion):
  https://www.notion.so/DayOne-End-to-End-Quality-Fulfillment-Standards-34ad8516232b81dd9e77c9e527d64663

## Message style
Professional, specific: always include order #, SKU, and the exact issue.
