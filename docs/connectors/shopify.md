# Shopify

**Status:** PLANNED — Phase 1

**Environment: staging/sandbox store only.** Do not point this connector at
the live production store under any circumstances until a separate,
explicit decision is recorded here — see Open questions for what's still
unconfirmed before this can even be wired up.

## Scope (planned)

Storefront MCP only, to start: product/catalog discovery, read-only. Shopify
ships four official MCP servers — pick up the others only if a phase
actually needs them:

| Server | Purpose | Notes |
|---|---|---|
| Storefront | Product discovery | On by default for Plus stores at `/.well-known/mcp/storefront`; no auth token required |
| Customer Account | Order history | One-click, reversible toggle in Shopify admin |
| Checkout | Cart operations | Write-capable — out of scope until a phase explicitly calls for it |
| Dev | Documentation access | Useful for agent-assisted Shopify dev work, not customer-facing |

## Auth

Storefront MCP needs no token on Plus. `SHOPIFY_STAGING_STOREFRONT_MCP_URL`
in `.env` is just the staging store's well-known endpoint — the env var
name is deliberately explicit about "staging" so it can't be confused with
a production URL at a glance.

## Open questions

- **Blocking:** what is the staging store's myshopify domain? Needed before
  this connector can be wired up at all — not guessing this, has to come
  from whoever owns the Shopify staging environment.
- Confirm the staging store is on Shopify Plus (Storefront MCP default-on
  requirement) — staging tier doesn't always mirror production tier.
- Confirm our (production) store is on Shopify Plus too, since that's what
  this connector eventually points at post-pilot.
- Decide if/when Customer Account MCP is worth enabling — it's read-only
  order history, low risk, but touches customer data so gets its own scope
  review rather than defaulting it on.
