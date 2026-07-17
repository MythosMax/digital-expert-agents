# Audit & observability

## Canonical events (MVP)

`run.started`, `plan.created`, `model.completed`,
`tool.proposed`, `approval.requested`, `approval.decided`,
`tool.started`, `tool.succeeded`, `tool.failed`,
`memory.read`, `run.completed`, `run.failed`, `run.cancelled`, `run.expired`

Do not log chain-of-thought. Store structured decision summaries, redacted
I/O, policy results, evidence refs, model/tool ids.

## Telemetry

- Traces: run root span; model / retrieval / approval / tool children
- Metrics: success, latency, tokens/cost, tool errors, approval time, denials
- Correlate Nest `traceId` with agent run id and Langfuse trace

Part harness: [`../harness/parts/dashboard.md`](../harness/parts/dashboard.md).
