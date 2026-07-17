# Part harness — Dashboard / Traces UI

## Purpose

React orchestration interface showing agent traces, task status, decisions,
and collaboration flows. Primary hackathon deliverable surface for judges.

## Code homes

- `apps/web/` (Next.js)
- Canonical event stream from `apps/agent-api`
- Design tokens from `packages/design-tokens/`

## MVP panels

| Panel | Data | Must show |
|---|---|---|
| Chat | SSE stream | User request + synthesized answer |
| Run timeline | Canonical events | Plan → tools → results |
| Collaboration graph | Graph state | Planner ↔ specialists |
| Task board | Run tasks | pending / running / done / failed |
| Tool inspector | Audit tool events | Redacted I/O + latency |
| Approval queue | HITL checkpoints | Approve / reject (when Phase 3) |
| Benchmark | Eval harness | Single vs multi comparison |

## In scope

- Consume canonical event union (not raw LangGraph vendor events)
- Correlation id visible end-to-end
- EN/VI copy for core labels
- Live update during a run

## Out of scope

- Editing agent prompts from the UI (MVP)
- Full banking product UI beyond agent demo shell
- Cards-heavy dashboard chrome that obscures the collaboration story

## Intake signals

`dashboard`, `trace UI`, `react-flow`, `timeline`, `orchestration interface`

## Default lane

- New event types / security-sensitive displays → **high-risk**
- Panel layout / visualization → **normal**
- Copy/i18n → **tiny**

## Context to read

1. This file
2. `docs/architecture/audit-observability.md`
3. `docs/product/dashboard.md`
4. `packages/design-tokens/` when styling

## Proof checklist

- [ ] Demo run visible without refreshing the whole page (stream or poll)
- [ ] Task board reflects all specialist tasks
- [ ] Collaboration graph shows ≥3 agents for demo scenario
- [ ] Tool inspector never shows secrets/PAN
- [ ] Same `traceId` links chat ↔ timeline

## Forbidden

- Rendering chain-of-thought as product truth
- Trusting client-side role checks for approvals
