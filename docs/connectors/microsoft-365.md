# Microsoft 365 / Agent 365

**Status:** RESEARCH — Phase 3

## What's available

Microsoft 365 Copilot supports MCP through Copilot Studio (GA since May
2025), with MCP tool calling extended into the Copilot chat surface by late
2025. The relevant piece for us is **Agent 365 MCP servers**: enterprise
MCP servers exposing deterministic, auditable tools for Outlook, Teams,
SharePoint, OneDrive, Dataverse, Word and more — through the Agent 365
tooling gateway. These offer capabilities not available via standard
Power Platform connectors.

## Blocker

Agent 365 MCP servers require the tenant to be enrolled in the **Microsoft
Frontier program** and a **full Microsoft 365 Copilot license** for the
users of the agent. Confirm both before planning any work here — this is
the gating item for Phase 3, not a technical integration question.

## Relevance to the Copilot Studio pilot

This is the most directly relevant connector to where the Copilot Studio
credits will actually get spent — SharePoint/Teams/Outlook agents are a
likely first real Copilot Studio use case. Treat Phase 3 here as the dry
run: what an agent can read/write in these surfaces, and how we'd monitor
it, before Copilot Studio makes it customer- or company-wide.

## Open questions

- Are we (or can we get) enrolled in Frontier?
- Which M365 Copilot licenses do we hold today, and do they cover Agent 365
  MCP usage?
- Once unblocked: which single surface (SharePoint likely, given
  Business-Central-adjacent document workflows) makes the best first
  target?
