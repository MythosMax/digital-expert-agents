# Part harness — Benchmark (single vs multi-agent)

## Purpose

Performance and quality comparison between a single-agent chatbot and the
multi-agent specialist system on the same cases.

## Code homes

- `tests/e2e/benchmark/`
- `docs/demo/benchmark-cases.md`
- Dashboard Benchmark panel (`apps/web`)
- Langfuse / OTel metrics

## Modes

| Mode | Behavior |
|---|---|
| `multi` | Planner + Credit + Legal + Ops |
| `single` | One agent with union of tools + corpora |

## Metrics (MVP)

| Metric | How |
|---|---|
| End-to-end latency | Trace duration |
| Token / cost | Provider + Langfuse |
| Task success | Eval rubric / expected checklist |
| Citation accuracy | Claims with valid provenance |
| Domain coverage | Did required domains run? |
| Unsafe action rate | Writes without approval (must be 0) |

## Case set

Minimum **5** cases spanning easy / medium / complex. Complex case must be
the credit-limit increase demo. See `docs/demo/benchmark-cases.md`.

## In scope

- Same fixtures and tools available to both modes
- Side-by-side table in dashboard or report markdown
- Deterministic case ids and recorded runs

## Out of scope

- Claiming statistical significance with tiny N
- Optimizing only for latency while dropping citations
- Different prompts that make the comparison unfair without documenting it

## Intake signals

`benchmark`, `single-agent`, `comparison`, `latency`, `eval`

## Default lane

- Changing success rubric / safety metrics → **high-risk**
- Adding cases → **normal**
- Report formatting → **tiny**

## Context to read

1. This file
2. `docs/demo/benchmark-cases.md`
3. `docs/harness/TEST_MATRIX.md`
4. `docs/product/success-metrics.md`

## Proof checklist

- [ ] ≥5 cases runnable in both modes
- [ ] Results table includes latency, tokens, success, unsafe rate
- [ ] Complex cross-domain case shows multi-agent coverage advantage or documents why not
- [ ] Unsafe action rate = 0 in both modes
- [ ] Case ids stable across runs

## Forbidden

- Hand-wavy "multi-agent is better" without numbers
- Hiding failed cases from the demo report
