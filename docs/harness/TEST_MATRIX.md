# Test Matrix

Maps product surfaces to minimum proof. Stories may require more; they must
not require less than this matrix for the touched surface.

## Surfaces

| Surface | Unit | Contract | Integration | E2E / Eval | Audit |
|---|---|---|---|---|---|
| Planner / orchestration | Graph transition helpers | Plan JSON schema | Crash/resume checkpoint | Complex request → 3 specialists | `plan.created` events |
| Specialist agents | Prompt/tool routing stubs | Agent contract load | Agent + tools + RAG | Domain-correct answer + citations | Agent id/version on events |
| Tools (read) | Schema validation | ToolSpec ↔ dispatcher | Call Nest `/v1/agent/*` | Tool result in UI timeline | `tool.succeeded` |
| Tools (write draft) | Idempotency key | Effect class + approval | Draft creates, no execute | HITL approve/reject paths | `approval.*` + `tool.*` |
| RAG | Chunker / filter | Retrieval port | Tenant+domain isolation | Citation present on claims | `memory.read` |
| Agent bridge | DTO mapping | OpenAPI / Zod | Scoped token authz | Agent cannot execute transfer | Ownership + rate limit |
| Dashboard | Component render | Event union decode | SSE stream consume | Trace tree + task board | Correlation id visible |
| Benchmark | Metric calculators | Case schema | Dual-mode runner | ≥5 cases single vs multi | Case id + mode on run |
| Security / HITL | Policy evaluate | HITL policy YAML | Interrupt/resume | Deny outside approval | Immutable decision record |

## Lane minimums

| Lane | Must run |
|---|---|
| Tiny | Targeted lint / doc check; no false claim of tests |
| Normal | Unit + relevant contract/integration for touched surface |
| High-risk | Full row for touched surfaces + security/red-team notes |

## Demo-critical happy path (must stay green)

1. User submits credit-limit increase request for CIF fixture
2. Planner creates ≥3 tasks assigned to Credit / Legal / Ops
3. Each specialist uses ≥1 tool and ≥1 RAG hit
4. Dashboard shows collaboration flow + timeline
5. Ops draft (if any) stops at HITL; no silent money move
6. Benchmark mode can re-run same case as single-agent

## Commands (fill when toolchain exists)

```text
# Placeholder — replace with real package scripts after scaffold
pnpm test --filter=...
pytest tests/
scripts/bin/harness-cli story verify-all
```
