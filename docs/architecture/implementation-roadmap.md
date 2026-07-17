# Implementation roadmap

Vertical slices with proof. Aligns with harness epics.

## Phase 0 — Decisions & baseline

- Product contract accepted
- Agent contracts drafted
- Demo scenario + fixtures named
- Architecture policy paths locked

**Exit:** boundaries, prohibited actions, human accountability approved.

## Phase 1 — Read-only tracer bullet

- Nest bootstrap + agent-bridge reads
- Agent-kernel contracts + one Credit read tool
- Agent-api run + SSE
- Dashboard timeline for one agent

**Exit:** no cross-tenant leak; answers have provenance; basic SLO ok.

## Phase 2 — Multi-agent + RAG

- LangGraph supervisor + 3 specialists
- Domain corpora ingested
- Collaboration graph + task board
- Complex demo request end-to-end

**Exit:** resume safe; 3 agents collaborate on one request; dashboard shows flow.

## Phase 3 — Write draft + HITL

- Ops draft tool + approval UI
- Idempotency + audit reconstruction
- Red-team skip-approval attempts

**Exit:** no write outside approval; duplicates safe.

## Phase 4 — Benchmark + polish

- Single vs multi mode
- ≥5 cases scored
- Docker one-command demo
- EN/VI core UI

**Exit:** comparison table + demo script ready for judges.

Definition of done per capability: contract, tests, metrics/audit, failure
runbook, kill switch where relevant.
