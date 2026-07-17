# EPIC-01 — Read-only tracer bullet

## Outcome

One Credit specialist can answer a credit question with a real read tool,
streamed to a basic dashboard timeline, via agent-bridge.

## In scope

- Nest agent-bridge read endpoints (accounts/credit summary)
- Agent-kernel contracts + Credit read tool
- Agent-api run start + SSE
- Dashboard timeline for one run

## Out of scope

- Multi-agent routing
- Write tools / HITL
- Full design polish

## Parts

`agent-bridge`, `specialist-agents`, `tools`, `dashboard`

## Lane

high-risk (auth + bridge)

## Acceptance

- [ ] Credit tool returns fixture data for CIF-12345
- [ ] Events visible on timeline
- [ ] Cookie auth rejected on `/v1/agent/*`
