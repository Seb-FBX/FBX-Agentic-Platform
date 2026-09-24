# FBX Agentic Platform

Furniturebox's working space for the agentic workflows pilot: standing up MCP
connectors across our systems (Business Central, Shopify, Zendesk, Qarma,
Microsoft 365), and learning how to spin up, monitor, manage and develop
agents on top of them — ahead of the Copilot Studio rollout.

## Why this repo exists

- Copilot Studio credits are inbound; we're mid-migration to Business Central.
- We want hands-on fluency with agents (build → monitor → manage → develop)
  before betting the Copilot Studio pilot on it.
- We already have one connector live: a Business Central MCP server scoped to
  **Sales, read-only**, used for QA. Everything here follows that same
  read-only-first pattern until a connector earns write access.

## Structure

```
CLAUDE.md                    Conventions for any Claude Code session working in this repo
.mcp.json                    MCP server registry (see docs/connectors for scope/status per server)
.env.example                 Placeholder env vars consumed by .mcp.json — copy to .env, never commit .env
docs/
  pilot-plan.md              Phased plan: sequencing, goals, exit criteria
  claude-code-best-practices.md   How we use Claude Code to build/monitor/manage agents here
  connectors/
    business-central.md      Status: LIVE (Sales, read-only)
    shopify.md                Status: PLANNED
    zendesk.md                Status: PLANNED
    qarma.md                  Status: RESEARCH (no public MCP server — likely custom build)
    microsoft-365.md          Status: RESEARCH (Agent 365 / Copilot Studio licensing dependent)
```

## Quick start

1. Read `CLAUDE.md` first — it sets the guardrails (read-only-first, secrets
   handling, how to onboard a new connector).
2. Read `docs/pilot-plan.md` for sequencing and what "done" looks like for
   each phase.
3. Copy `.env.example` to `.env` and fill in credentials for whichever
   connector you're working with locally. Never commit `.env`.
4. Each connector's doc in `docs/connectors/` tracks its own status, scope,
   auth method and open questions — update it as the connector moves from
   research → configured → live.
