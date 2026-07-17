# Security & deployment

## Controls

- Scoped agent JWT; no user cookies for agents
- Tool allowlists + domain re-check
- HITL for writes; agents draft only
- Tenant isolation on RAG and DB
- Rate limits on `/v1/agent/*`
- Kill switch for agent runs
- PII redaction in logs/traces

## Topology (hackathon UAT)

```text
docker compose:
  web | api | agent-api | agent-worker | postgres(pgvector) | redis | langfuse(optional)
```

Single-host Compose is enough for demo. Do not invent K8s unless a story asks.

Part harness: [`../harness/parts/security-hitl.md`](../harness/parts/security-hitl.md),
[`../harness/parts/agent-bridge.md`](../harness/parts/agent-bridge.md).
