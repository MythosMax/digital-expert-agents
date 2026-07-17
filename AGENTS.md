# Agent Instructions

This is the **Digital Expert Agents** monorepo for SHB banking operations:
planner + specialist agents (Credit, Legal/Compliance, Operations), tool use,
domain RAG, HITL write boundary, and a React orchestration dashboard.

## Project rules

1. Prefer `docs/architecture/` and `STRUCTURE.md` over inventing new layering.
2. `packages/` = platform (kernel, runtime, shared). `modules/` = domain
   business truth + `agent-tools/`. Do not put domain aggregates in `packages/`.
3. Backend banking API (`apps/api`) is NestJS. Agent runtime (`apps/agent-api`,
   `apps/agent-worker`) is Python/LangGraph. Wire them via the agent-bridge
   contract — agents never hold user cookies.
4. Write/money-moving actions require HITL approval. Agents draft; humans
   confirm via the normal banking flow.
5. Architecture form templates live in root `templates/`. Story packets live in
   `docs/stories/`. Harness story templates live in `docs/templates/`.
6. Do not commit secrets (`.env`, credentials, `harness.db`).
7. Every specialist agent must have a filled agent contract under
   `config/agents/` before implementation.

## Harness

Before material work, read:

- `README.md`
- `docs/harness/HARNESS.md`
- `docs/harness/FEATURE_INTAKE.md`
- `docs/harness/CONTEXT_RULES.md`
- `docs/product/README.md`
- `STRUCTURE.md`
- `docs/architecture/index.md` (when touching agent architecture)
- Relevant part harness under `docs/harness/parts/`

Change workflow:

```text
intake (type + lane)
  -> work-item hierarchy (spec/epic/story/task)
  -> bounded implementation
  -> proof flags / validation
  -> trace (+ backlog if friction)
```

## Part ownership (read the matching harness part)

| Part | Harness doc | Code home |
|---|---|---|
| Planner / orchestration | `docs/harness/parts/orchestration.md` | `packages/runtime-langgraph`, `apps/agent-worker` |
| Specialist agents | `docs/harness/parts/specialist-agents.md` | `modules/{credit,legal,operations}`, `config/agents` |
| Tool use | `docs/harness/parts/tools.md` | `modules/*/agent-tools`, `packages/governance` |
| RAG / knowledge | `docs/harness/parts/rag.md` | `modules/knowledge`, `data/knowledge` |
| Agent bridge / banking API | `docs/harness/parts/agent-bridge.md` | `apps/api` |
| Dashboard / traces | `docs/harness/parts/dashboard.md` | `apps/web` |
| Benchmark (single vs multi) | `docs/harness/parts/benchmark.md` | `tests/e2e`, `docs/demo` |
| Security / HITL | `docs/harness/parts/security-hitl.md` | `packages/governance`, `config/policies` |
