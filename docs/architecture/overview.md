# Overview

## Capabilities

| Capability | Owner |
|---|---|
| Chat + orchestration dashboard | `apps/web` |
| Banking domain + agent bridge | `apps/api` |
| Run lifecycle / stream | `apps/agent-api` + agent-kernel |
| Multi-agent graph | `apps/agent-worker` + runtime-langgraph |
| Policy / HITL / budgets | `packages/governance` |
| Domain truth + tools | `modules/{credit,legal,operations}` |
| RAG corpora | `modules/knowledge` + `data/knowledge` |

## Standard execution loop

1. Channel authenticates actor; builds `ExecutionContext` (tenant, actor,
   permissions, correlation id, deadline).
2. Application loads minimal context per policy.
3. Planner chooses deterministic graph path (MVP) with bounded model nodes.
4. Dispatcher verifies allowlist, schema, budget, permission.
5. Risky writes stop at durable HITL checkpoint.
6. Domain callee re-checks rights; executes idempotently; emits audit events.
7. Runtime checkpoint saves resume state; product state stays in platform/domain.
8. Canonical events stream to UI.

## Reliability envelope

- Max steps, wall-clock timeout, token/cost budget, tool-call rate
- Allowed data classes per model/provider
- Recovery: model timeout, tool timeout, approval expiry, worker crash
- Idempotency + compensation for external writes
- SLO: first token, completion, approval wait, recovery, audit availability
