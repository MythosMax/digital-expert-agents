# Product contract — Digital Expert Agents

Accepted problem: multi-agent digital specialists for SHB banking operations
that plan, use tools, retrieve domain knowledge, collaborate, and take bounded
actions — with a dashboard of traces and a single- vs multi-agent comparison.

## Goals

1. Demonstrate operational GenAI beyond Q&A
2. Coordinate Credit + Legal + Operations on one complex request
3. Keep banking controls (authz, HITL, audit)
4. Show measurable value vs single-agent chatbot

## Non-goals (MVP)

- Full production loan origination system
- Real NHNN connectivity
- Agent-executed payments
- Unbounded autonomous loops without budgets

## Personas

| Persona | Need |
|---|---|
| Relationship / credit officer | Faster cross-functional assessment |
| Compliance reviewer | Evidence-backed regulatory checks |
| Operations staff | Drafted next actions, not opaque text |
| Judge / hackathon | Clear architecture + live demo + metrics |

## Deliverables map

| Deliverable | Product doc | Part harness |
|---|---|---|
| 3 specialists | [`agents.md`](agents.md) | specialist-agents |
| Planner | [`orchestration.md`](orchestration.md) | orchestration |
| Tools | [`tools.md`](tools.md) | tools |
| RAG | [`knowledge.md`](knowledge.md) | rag |
| Bridge | [`agent-bridge-contract.md`](agent-bridge-contract.md) | agent-bridge |
| Dashboard | [`dashboard.md`](dashboard.md) | dashboard |
| Benchmark | [`success-metrics.md`](success-metrics.md) | benchmark |
| Demo | [`demo-scenario.md`](demo-scenario.md) | — |

## Success metrics

See [`success-metrics.md`](success-metrics.md).
