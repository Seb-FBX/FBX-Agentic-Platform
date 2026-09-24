# Business Central

**Status:** LIVE — Sales, read-only

## Scope

Read-only access to the Sales area, used for QA today. This is the
reference pattern for every other connector in this pilot: narrowest useful
scope first, write access only as a deliberate, documented upgrade.

## Auth

Bearer token via `BC_MCP_SALES_RO_TOKEN` (see `.env.example`). Rotate per
whatever policy the BC admin center enforces; do not widen the token's
underlying permissions without updating this doc first.

## Notes / options considered

- Microsoft's native Business Central MCP server (2026 Wave 1) now exposes
  650k+ actions across sales, finance, supply chain, HR, field service and
  project ops, with OAuth 2.1 and Purview audit integration — far broader
  than what we're using. Worth revisiting in Phase 3 once we decide which
  additional areas (if any) are worth agent-enabling post-migration.
- There's also a separate **admin center MCP** (environment management) and
  a **troubleshooting MCP for AL** (dev-focused) — neither relevant to this
  pilot's current goals, noted here in case a future dev workflow wants them.

## Open questions

- Does the Business Central migration change the MCP endpoint or token
  scoping we currently depend on? Confirm before the migration cuts over.
- What's the actual exit criteria for granting write scope (e.g. sales
  order creation)? Not yet decided — track in Phase 3 of the pilot plan.
