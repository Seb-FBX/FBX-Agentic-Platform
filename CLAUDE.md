# CLAUDE.md

Conventions for any Claude Code session (local or on the web) working in this
repository. This repo is the staging ground for Furniturebox's agentic
workflows pilot — it holds MCP connector configs, connector docs, and the
pilot plan, not application code (unless a connector genuinely needs a
custom MCP server, in which case it gets its own subfolder and its own
CLAUDE.md).

## Guardrails

- **Read-only first.** Every new connector starts scoped read-only against
  the narrowest resource it needs (mirror the Business Central "Sales,
  read-only" pattern). Write scope is a deliberate, documented upgrade in
  that connector's doc under `docs/connectors/`, not a default.
- **Non-production first.** Every new connector points at a staging/sandbox
  environment by default, never the live/production instance, until its
  connector doc records an explicit, reviewed decision to point at
  production. Name env vars and MCP server keys so the target environment
  is unambiguous (e.g. `SHOPIFY_STAGING_STOREFRONT_MCP_URL`, not a bare
  `SHOPIFY_STOREFRONT_MCP_URL` that could silently mean either).
- **No real credentials in the repo.** `.env` is gitignored. `.mcp.json`
  only ever references environment variables (`${VAR_NAME}`), never literal
  keys, tokens, or tenant IDs. If you ever see a real secret about to be
  committed, stop and flag it rather than pushing.
- **One connector, one doc.** Before wiring up a new MCP server, add or
  update its file in `docs/connectors/`: status, scope, auth method, owner,
  open questions. Update the status line when it moves between
  research → configured → live.
- **Prefer official/maintained MCP servers** over ad-hoc ones where they
  exist and fit the scope needed; note the alternative(s) considered in the
  connector doc even when you don't pick them.

## Working conventions

- Commit messages: describe the connector/doc change and why, not a diary of
  steps taken.
- Keep `docs/pilot-plan.md` current — if a phase's scope or sequencing
  changes, update it in the same change, not as a follow-up.
- This repo is a learning environment for the pilot, so favour clarity and
  small, reviewable changes over building out infrastructure ahead of need.
