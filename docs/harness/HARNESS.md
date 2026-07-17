# Harness

Harness is the repository-level operating model for turning the Digital Expert
Agents problem statement into bounded, validated work.

The app is what judges and bankers touch. Harness is what humans and coding
agents use to understand scope, choose proof, track progress, and leave evidence.

## Operating loop

```text
problem statement / human intent
  -> feature intake
  -> product contract
  -> work item hierarchy (spec → epic → story → task)
  -> story / spike / task execution
  -> validation proof
  -> durable progress update
  -> trace or backlog record
```

Every task can produce two outputs:

- **Product delta:** app code, tests, API shape, agent contracts, knowledge docs.
- **Harness delta:** docs, templates, validation expectations, backlog items.

## Agent orchestration (coding agents)

Conductor model for multi-agent coding work:

- Conductor owns planning, assignment, integration, validation, status updates.
- A sub-agent owns exactly one task at a time.
- Sub-agents do not implement whole epics.
- Each delegated task needs: parent story, bounded write scope, out-of-scope,
  expected proof.
- New work discovered → report up; conductor creates new task/story/backlog.

## Part harnesses

This repo splits control by product part. Always open the matching part doc
before implementing that surface:

| Part | Doc |
|---|---|
| Orchestration / planner | [`parts/orchestration.md`](parts/orchestration.md) |
| Specialist agents | [`parts/specialist-agents.md`](parts/specialist-agents.md) |
| Tools | [`parts/tools.md`](parts/tools.md) |
| RAG / knowledge | [`parts/rag.md`](parts/rag.md) |
| Agent bridge / banking API | [`parts/agent-bridge.md`](parts/agent-bridge.md) |
| Dashboard | [`parts/dashboard.md`](parts/dashboard.md) |
| Benchmark | [`parts/benchmark.md`](parts/benchmark.md) |
| Security / HITL | [`parts/security-hitl.md`](parts/security-hitl.md) |

## Source of truth

| Surface | Purpose |
|---|---|
| `docs/product/` | Accepted product contract |
| `docs/stories/` | Epic / story / spike packets |
| `docs/harness/parts/` | Per-part intake, proof, context rules |
| `config/agents/` | Agent contracts (reviewed) |
| `config/policies/` | HITL / allowlist / budget policies |
| `scripts/schema/` | Harness SQLite migrations (when CLI present) |
| `harness.db` | Local operational records (gitignored) |

## Risk lanes

| Lane | When | Trace tier |
|---|---|---|
| Tiny | Copy/docs/config with no behavior change | Minimal |
| Normal | Feature behavior within an existing contract | Standard |
| High-risk | Auth, money, cross-tenant, agent write tools, architecture | Detailed |

See [`FEATURE_INTAKE.md`](FEATURE_INTAKE.md), [`TRACE_SPEC.md`](TRACE_SPEC.md),
[`CONTEXT_RULES.md`](CONTEXT_RULES.md), [`TEST_MATRIX.md`](TEST_MATRIX.md).

## Closed-loop harness evolution

```text
trace friction / verifier failure
  -> failure attribution
  -> proposal
  -> held-in / held-out eval
  -> promote or reject
```

Do not promote a harness behavior change unless held-out evals do not regress.
