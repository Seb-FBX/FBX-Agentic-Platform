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

**Checked, endpoint not live yet:** with network access to `*.myshopify.com`
allowed, the endpoint responds — but with the store's maintenance/password
page (HTML, storefront-password prompt), not an MCP manifest. Most likely
cause: the staging store has storefront password protection enabled (common
for staging so it isn't publicly browsable), and an unauthenticated request
to `/.well-known/mcp/storefront` gets caught by that gate the same as any
other page. Untested alternative explanation: the store isn't on Shopify
Plus, so Storefront MCP isn't enabled at all — needs ruling out too.

## Open questions

- **Blocking:** does storefront password protection block Storefront MCP's
  well-known endpoint? If so, is there a supported way to exempt it (Shopify
  admin setting) or do we need the store's storefront password itself —
  and if the latter, how does that get supplied to an MCP client without
  becoming a credential we'd have to manage outside `.env`'s current shape.
- Confirm the staging store is on Shopify Plus (Storefront MCP default-on
  requirement) — staging tier doesn't always mirror production tier.
- Confirm our (production) store is on Shopify Plus too, since that's what
  this connector eventually points at post-pilot.
- Decide if/when Customer Account MCP is worth enabling — it's read-only
  order history, low risk, but touches customer data so gets its own scope
  review rather than defaulting it on.
