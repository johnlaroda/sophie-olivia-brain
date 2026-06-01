---
name: so-refund
description: Use when a Sophie & Olivia ticket needs a refund or store-credit decision. Checks policy + precedent, then DRAFTS the #ops-return approval post AND the customer reply to ops/drafts/. Never issues a refund or sends anything.
---

# so-refund — Draft a Refund Request + Customer Reply (read & draft only)

## Trust
READ & DRAFT ONLY. Never issue a refund, never post to #ops-return, never send the
customer reply. Output is a draft file for John to review, approve, and send.

## Inputs
- A Gorgias ticket (id) involving a refund / return / exchange request.

## Steps
1. Read context/policies.md, context/precedents.md, context/brand-voice.md, context/products.md.
2. Fetch the ticket via Gorgias MCP; pull the related order from Shopify (order #, items, amount, date).
3. Check eligibility against policy: 30-day return window, 14-day exchange→store credit,
   condition rules, who pays return shipping. Note if the request is outside policy.
4. Search context/precedents.md and Slack #ops-return for similar past decisions.
5. Form a recommendation — refund / store credit / exchange / deny — with reasoning. If the
   case is unclear or outside policy, mark "NEEDS JOHN" at the top and do not assume an outcome.
6. Write BOTH of these into ops/drafts/YYYY-MM-DD-refund-ticket-<id>.md:
   a) the #ops-return post: order #, ticket #, customer issue summary, amount, your recommendation.
   b) the customer reply in brand voice (sign-off: "Regards, Sophie & Olivia Customer Support Team").
   Add a short "sources checked" list.
7. Append a line to today's logs/ file: ticket id, refund amount, recommendation.

## After John decides
Once John approves/denies, draft the matching entry for context/precedents.md so future
drafts stay consistent (John adds it).

## Never
Issue the refund, post to #ops-return, or send the customer reply. John does all of that.
