# Setup To-Dos / Known Limitations

Action items to unlock fuller capability. Newest first.

## 🔴 Shopify connector missing `read_shopify_payments` scope
**Flagged:** 2026-06-01 (surfaced during the Lucia Chemise analysis).

**Problem:** The Shopify MCP connector cannot query `shopifyPaymentsAccount`
(disputes API) — it returns *"Access denied. Required access: the
`read_shopify_payments` or `read_shopify_payments_accounts` access scope."*

**Impact on analyses:**
- Cannot pull chargeback/dispute **dollar amounts**, **reason codes**, or **win/loss
  rates** directly. We can only see order-level dispute *presence* (WON/LOST) via the
  `orders { disputes }` field — enough to tell *which* SKUs get disputed, but not how
  much money or why.
- **PayPal disputes** are not exposed through the current connectors at all and remain
  a separate blind spot.

**Fix:** Add the `read_shopify_payments` (and/or `read_shopify_payments_accounts`)
scope to the Shopify connector/app, then reconnect. After that, dispute/chargeback
analyses (e.g. so-report, product quality deep-dives) can include A$ values, reason
codes, and win rates.

**Where:** Shopify Admin → Settings → Apps and sales channels → (the connected app) →
review/approve scopes; or re-authorize the connector at claude.ai/customize/connectors
once the scope is added.

**Until fixed:** dispute analyses will note this gap and fall back to order-level
dispute presence only.

---

## Other open items (lower priority)
- `context/products.md` — add the exact size-chart link + per-line band/cup conversion
  once finalised with DayOne.
- `context/team.md` — fill in remaining team members + roles.
- PayPal dispute visibility — no connector currently exposes it; revisit if PayPal
  volume grows.
