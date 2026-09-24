# Qarma

**Status:** RESEARCH — Phase 4

## What Qarma actually is

Qarma is a supply-chain **quality inspection and compliance** platform —
quality inspections, supplier audits & corrective actions, product
compliance documentation. Not a customer-service QA tool (easy to confuse
given the acronym-shaped name). Relevant to Furniturebox's sourcing/QC
side, not support.

## Current state

No public MCP server exists for Qarma today (checked September 2026). This
is deliberately the last connector in the pilot — build only once Phases
1–3 have established our config, auth and doc conventions on integrations
that already exist.

## Plan

1. Confirm whether Qarma exposes a documented API (REST or otherwise) and
   what auth it supports.
2. If yes: scope a thin, read-only custom MCP server (e.g. inspection
   results, audit findings) — no write access to compliance records from an
   agent, ever, without a separate explicit decision given the regulatory
   surface.
3. If no API exists, or access requires a commercial add-on, record that
   here and park the connector rather than building against an
   unsupported/private interface.

## Open questions

- Do we have (or can we get) API access to Qarma at all?
- Who owns the Qarma relationship internally, to sanity-check any custom
  integration before it touches production inspection/audit data?
