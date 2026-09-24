# Shopify

**Status:** PLANNED — Phase 1

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

Storefront MCP needs no token on Plus. `SHOPIFY_STOREFRONT_MCP_URL` in
`.env` is just the store's well-known endpoint.

## Open questions

- Confirm our store is on Shopify Plus (Storefront MCP default-on
  requirement).
- Decide if/when Customer Account MCP is worth enabling — it's read-only
  order history, low risk, but touches customer data so gets its own scope
  review rather than defaulting it on.
