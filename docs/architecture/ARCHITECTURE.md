# Architecture (one-pager)

Digital Expert Agents separates **business decision ownership** from **agent
runtime mechanisms**. Models propose and plan; the platform owns identity,
policy, product state, approvals, audit, and side effects.

```mermaid
flowchart TB
  UI[apps/web - Chat + Dashboard]
  Nest[apps/api - Banking + /v1/agent bridge]
  AgentAPI[apps/agent-api]
  Worker[apps/agent-worker - LangGraph]
  Plan[Planner]
  C[Credit]
  L[Legal]
  O[Ops]
  Gov[governance + HITL]
  KB[(knowledge corpora)]
  DB[(PostgreSQL + Redis + pgvector)]

  UI --> AgentAPI
  UI --> Nest
  AgentAPI --> Worker
  Worker --> Plan
  Plan --> C
  Plan --> L
  Plan --> O
  C --> Gov
  L --> Gov
  O --> Gov
  C --> KB
  L --> KB
  O --> KB
  Gov --> Nest
  Nest --> DB
  Worker -->|canonical events| UI
```

## Non-negotiables

1. Runtime framework is not system of record.
2. All access is tenant-scoped; domain re-checks authz.
3. Write tools need approval by risk, idempotency, immutable audit.
4. Checkpoint ≠ durable business memory.
5. Prompts do not hold business rules that must be correct — put those in testable code/tools.
6. Agents never hold user session cookies.
