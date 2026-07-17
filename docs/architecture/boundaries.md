# Boundaries

See also [`../../STRUCTURE.md`](../../STRUCTURE.md).

## Dependency rules

1. `packages/*` must not import `modules/*` (except via `apps/composition`).
2. Runtime adapters implement ports; do not import domain implementations.
3. Modules publish tools via `agent-tools/`; composition collects them.
4. Tool closures call public surfaces (Nest `/v1/agent/*` or module application).
5. Public APIs must not expose LangGraph/LangChain vendor types.
6. Web talks to Nest and agent-api only — never to worker internals.

## Trust boundaries

| Boundary | Control |
|---|---|
| Browser → Nest | Cookie session + CSRF + handshake (banking UI) |
| Agent → Nest | Scoped service JWT on `/v1/agent/*` |
| Worker → tools | Dispatcher allowlist + governance |
| Retrieval → prompt | Hard tenant/domain filter; untrusted text |

## Prohibited shortcuts

- Agent using user cookie
- Specialist calling another specialist's private tools without planner
- Shared undifferentiated RAG index in "production demo" mode
- Silent write without audit event
