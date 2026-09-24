# Using Claude Code for This Pilot

How we're using Claude Code itself as part of getting familiar with
spinning up, monitoring, managing and developing agentic systems — separate
from the connectors it's helping us build.

## Why Claude Code, specifically, for this pilot

It gives us the full lifecycle in one tool: configure an MCP connector,
converse with it to validate scope/behaviour, iterate on the config, and
version-control all of it — which is exactly the loop we'll need once
Copilot Studio is in the mix, just with a faster iteration cycle and
without needing a maker license to experiment.

## Conventions for this repo

- **MCP config lives in `.mcp.json`, secrets live in `.env`.** Never the
  reverse. This mirrors how Copilot Studio separates connector config from
  credentials, so the habits transfer.
- **One session, one connector (usually).** Keep changes scoped to a single
  connector/doc pair so history stays legible — matches the phased pilot
  plan rather than trying to wire up everything at once.
- **CLAUDE.md is the guardrail file.** Anyone (or any session) picking up
  work here should read it first; keep it short and update it when a
  convention actually changes, not preemptively.
- **Use subagents for research, not for connector wiring.** Exploring "what
  MCP servers exist for X" is a good fit for a research subagent; actually
  editing `.mcp.json` and connector docs should happen in the main session
  so the reasoning is visible in this conversation.

## Monitoring & managing agents day to day

- Treat each connector doc's status line (RESEARCH / PLANNED / CONFIGURED /
  LIVE) as the source of truth for where things stand — don't rely on chat
  history to reconstruct state.
- When something misbehaves against a live connector, the first move is
  narrowing scope further (drop to a smaller resource set) before
  debugging logic — cheaper to rule out an over-broad grant than to chase a
  false lead.
- Before granting write access to any connector, write down in its doc
  what "safe to fail" looks like for that action (reversible? auditable?
  blast radius if wrong?). If you can't answer that, it's not ready for
  write scope yet.

## Where to go deeper

- The `claude-code-guide` agent (available via the Agent tool in this
  environment) answers specific "can Claude Code do X" questions — hooks,
  settings, MCP server configuration mechanics — better than re-deriving it
  here.
- Anthropic's own Claude Code docs are the canonical reference for anything
  this file doesn't cover; keep this file to Furniturebox-specific
  conventions rather than duplicating general documentation.
