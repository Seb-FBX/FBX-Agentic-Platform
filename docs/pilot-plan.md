# Agentic Workflows Pilot Plan

## Goal

Build hands-on fluency with agents — how to spin up, monitor, manage and
develop them — across the systems we actually run on, ahead of committing
the incoming Copilot Studio credits to a specific workflow. Business
Central migration is happening in parallel, so BC is both a live target and
a moving one: keep connector scope narrow so it survives the migration.

## Principles

- **Read-only before write, one system before the next.** Prove monitoring
  and management on a low-risk connector before granting write scope or
  adding a second connector.
- **Staging before production, always.** Every connector wires up against a
  staging/sandbox environment first; moving a connector to production is a
  separate, explicit decision recorded in that connector's doc, never a
  side effect of the pilot moving forward.
- **Reuse before build.** Prefer an existing, maintained MCP server; only
  build custom (Qarma) once the reuse options are genuinely exhausted.
- **Every connector lands in `docs/connectors/`** with its status kept
  current, so the pilot's real state is legible without reconstructing it
  from chat history.

## Phases

### Phase 0 — Baseline (done)
Business Central MCP, Sales, read-only, used for QA. This is the reference
pattern for every connector that follows.

### Phase 1 — Second connector, low risk
Bring up **Shopify Storefront MCP** against the **staging store** (read-only,
no auth token required on Plus stores) as the second data point. Goal:
confirm the read-only-first, staging-first pattern generalises to a
completely different vendor and auth model before touching anything with
customer PII, write access, or the production store.

Exit criteria: an agent can answer product/catalog questions against
staging Shopify data, we've documented what monitoring that connection in
practice actually looks like (logs, rate limits, failure modes), and moving
to production is recorded as its own explicit follow-on decision rather
than assumed.

### Phase 2 — Support surface
Bring up **Zendesk** (read-only: tickets, Help Center) once an MCP
implementation is chosen and vetted (see `docs/connectors/zendesk.md`).
Zendesk carries customer PII, so this phase also exercises the auth model
(per-user OAuth 2.1 PKCE) properly rather than a shared token, and any
scope beyond read triage needs an explicit decision recorded in the
connector doc.

Exit criteria: an agent can triage/summarise tickets read-only; PII handling
and access scoping are written down, not assumed.

### Phase 3 — Microsoft ecosystem
Revisit **Business Central write scope** (post-migration) and **Microsoft
365 / Agent 365** (Teams, SharePoint, Outlook) once licensing/Frontier
enrollment is confirmed. This is the phase most directly relevant to the
Copilot Studio rollout, so treat it as the dry run for what Copilot Studio
agents will actually be allowed to do.

Exit criteria: a documented decision on which BC write actions (if any) are
safe to agent-enable, and a working MCP connection into at least one
Microsoft 365 surface.

### Phase 4 — Qarma (custom build)
No public MCP server exists for Qarma. Once Phases 1–3 have established the
patterns for config, monitoring and doc hygiene, evaluate whether Qarma's
API supports a thin custom MCP server (quality inspections / supplier audit
data, read-only to start). This is deliberately last — it's the only
connector requiring us to build rather than integrate.

## Out of scope for now

- Any Copilot Studio-specific build — this repo is the pre-work, not the
  Copilot Studio implementation itself.
- Write access on any connector until its corresponding read-only phase has
  a documented exit.
