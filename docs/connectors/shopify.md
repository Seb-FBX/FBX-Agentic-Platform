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

## Staging store

Confirmed: `staging-furniturebox-uk` (myshopify domain
`staging-furniturebox-uk.myshopify.com`), per the Shopify admin URL
`https://admin.shopify.com/store/staging-furniturebox-uk/orders`. Storefront
MCP endpoint is therefore
`https://staging-furniturebox-uk.myshopify.com/.well-known/mcp/storefront`,
set locally as `SHOPIFY_STAGING_STOREFRONT_MCP_URL` in `.env` (gitignored,
not committed).

**Not yet verified:** whether that endpoint actually responds (i.e. the
staging store is on Shopify Plus with Storefront MCP enabled). A check from
this session was blocked by the environment's network egress policy
(`*.myshopify.com` not in the allowed hosts) — needs either that host
allowed in the environment's network settings, or a manual check from
somewhere with access.

## Open questions

- Confirm the staging store is on Shopify Plus (Storefront MCP default-on
  requirement) — staging tier doesn't always mirror production tier.
- Confirm our (production) store is on Shopify Plus too, since that's what
  this connector eventually points at post-pilot.
- Decide if/when Customer Account MCP is worth enabling — it's read-only
  order history, low risk, but touches customer data so gets its own scope
  review rather than defaulting it on.
