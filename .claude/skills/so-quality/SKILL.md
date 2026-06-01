---
name: so-quality
description: Use when a Sophie & Olivia ticket reports a product defect or quality issue (not just fit/sizing). Drafts a #dayone-quality report and a customer reply to ops/drafts/. Never sends.
---

# so-quality — Draft a Quality/Defect Report (read & draft only)

## Trust
READ & DRAFT ONLY. Never post to Slack or message the customer. Output is a draft for John.

## Inputs
- A Gorgias ticket reporting a defect / quality problem.

## Steps
1. Read context/suppliers.md, context/products.md, context/brand-voice.md.
2. Fetch the ticket and any photos via Gorgias; pull the order/SKU from Shopify.
3. Distinguish a genuine quality defect (material / stitching / construction) from a sizing
   complaint. If it is really sizing, stop and hand off to so-support / so-refund instead.
4. Search #dayone-quality for prior reports of the same SKU/batch so you don't duplicate.
5. Write into ops/drafts/YYYY-MM-DD-quality-ticket-<id>.md:
   a) the #dayone-quality report: order #, SKU/product, defect description with specifics,
      photo references, customer impact, and whether it counts toward the 1.5% defect cap.
   b) a customer reply in brand voice (sign-off: "Regards, Sophie & Olivia Customer Support Team").
   Add a short "sources checked" list.
6. Append a line to today's logs/ file: ticket id, SKU, defect summary.

## Never
Post to #dayone-quality or message the customer. John sends.
