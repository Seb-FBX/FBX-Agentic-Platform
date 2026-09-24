# Zendesk

**Status:** PLANNED — Phase 2

## Scope (planned)

Read-only: tickets, ticket comments, Help Center articles. No public write
(comment/tag/status changes) until this doc records an explicit decision to
enable it.

## Implementation options (no single official MCP server exists)

| Option | Notes |
|---|---|
| Zendesk Marketplace "MCP Server" app | Vendor-listed in the Zendesk Marketplace; check current review/maintenance status before relying on it |
| `reminia/zendesk-mcp-server` (open source) | Ticket + comment + attachment read/write tools; check license and last-commit recency before adopting |
| Digital4Better MCP server | Two-way: Help Center search/draft/translate plus Support ticket management end-to-end — broader than we need for Phase 2 |

Default plan: start with whichever option supports read-only ticket +
Help Center access with the least additional scope, and record the actual
choice here once tested (update this table's status, don't just pick
silently in `.mcp.json`).

## Auth

Per-user OAuth 2.1 PKCE where the implementation supports it, so the agent
only ever sees what the authenticating agent/user can see — do not fall
back to a shared API token unless a specific implementation requires it,
and note that tradeoff here if so.

## Open questions

- PII handling: tickets contain customer PII by default. Confirm data
  retention/logging behaviour of whichever MCP server we pick before Phase
  2 goes live, not after.
- Which implementation did we land on, and why? Fill in once decided.
