# Trace Specification

Traces record what happened during a harness task. Depth must match the risk
lane. Format follows the agent-flatform TRACE_SPEC pattern.

## Required fields by tier

### Minimal (tiny)

- `task_summary` (≥ 10 chars)
- `outcome`: `completed` | `blocked` | `partial` | `failed`

### Standard (normal)

All Minimal, plus:

- `intake_id` / `story_id` when applicable
- `agent`
- `actions_taken` (JSON array text)
- `files_read`, `files_changed`
- At least one of `errors` or `harness_friction`

### Detailed (high-risk)

All Standard, plus:

- `decisions_made`
- `errors` (`none` if none)
- `harness_friction` (`none` only after checking)
- `duration_seconds` or note why unavailable
- `token_estimate` or note why unavailable
- `notes` when multi-story / skipped validation

## Lane mapping

| Lane | Expected tier |
|---|---|
| Tiny | Minimal (Standard if harness docs or friction) |
| Normal | Standard |
| High-risk | Detailed |

## Friction capture

Populate `harness_friction` when:

- Missing / contradictory source of truth
- Required validation unclear or unavailable
- Repeated manual step that should become a template
- Out-of-scope finding that should become backlog
- Benchmark failure not attributable to a component

## Failure attribution categories

- `missing_story_packet`
- `missing_validation`
- `missing_artifact`
- `context_gap`
- `tool_retry_loop`
- `scope_expansion`
- `verification_skipped`
- `unlinked_work_state`
- `agent_hallucination` (product-agent eval)
- `cross_tenant_risk`

## Review checklist

- Tier matches lane
- `files_changed` matches reality
- Part harness proof items addressed or explicitly deferred
- Friction that should become work is in backlog
