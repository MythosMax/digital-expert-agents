# EPIC-02 — Multi-agent + RAG + dashboard

## Outcome

Planner + Credit + Legal + Ops collaborate on the credit-limit increase demo
with domain RAG and collaboration UI.

## In scope

- LangGraph supervisor
- 3 specialists + domain corpora
- Collaboration graph + task board
- Demo scenario E2E

## Out of scope

- Write execution
- Full benchmark suite (starts in EPIC-04)

## Parts

`orchestration`, `specialist-agents`, `rag`, `dashboard`, `tools`

## Lane

high-risk (architecture + multi-agent)

## Acceptance

- [ ] ≥3 specialist tasks created for demo request
- [ ] Each specialist ≥1 tool + ≥1 RAG hit
- [ ] Dashboard shows graph + tasks + timeline
