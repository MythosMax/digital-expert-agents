# Part harness — Security / HITL

## Purpose

Guardrails and human-in-the-loop so agents can propose work without bypassing
banking controls. Platform owns approval truth; runtime only pauses/resumes.

## Code homes

- `packages/governance/`
- `config/policies/` (HITL, budgets, allowlists)
- `templates/hitl-policy.template.yaml`
- Dashboard approval queue
- Agent-bridge token scopes

## When human must decide

- Any `write_*` tool per policy
- Confidence below threshold or contradictory evidence
- Scope/cost exceeds budget
- Plan change that increases risk
- Sensitive data needing new purpose/consent
- No deterministic recovery path

## Approval record (minimum fields)

`actor`, `approver policy`, `proposed action`, `sanitized params`, `expected effect`,
`evidence`, `risk`, `expiry`, `decision`, `reason`, `timestamps`, correlation ids

## Decision semantics

| Decision | Behavior |
|---|---|
| Approve once | Exact action hash + idempotency key only |
| Edit and approve | New proposal; re-validate; audit both |
| Reject | Terminal or defined back-edge; no silent rephrase retry |
| Expire / cancel | No execution; terminal reason |

## Guardrail layers

1. Input: auth, size, DLP / injection signals
2. Planning: allowlist, budgets, max steps
3. Pre-tool: schema, permission, approval, rate limit
4. Post-tool: validate, redact, reconcile, audit
5. Response: policy filter, provenance, no secret leakage

## Intake signals

`HITL`, `approval`, `guardrail`, `kill switch`, `risk tier`

## Default lane

Always treat policy/HITL/authz changes as **high-risk**.

## Context to read

1. This file
2. `docs/architecture/hitl-guardrails.md`
3. `docs/harness/parts/tools.md`
4. `docs/harness/parts/agent-bridge.md`
5. Active HITL policy YAML

## Proof checklist

- [ ] Write tool cannot succeed without required approval
- [ ] Expired approval cannot be resumed into execution
- [ ] Duplicate approve does not double-write
- [ ] Kill switch stops new runs
- [ ] Audit reconstructs who approved what
- [ ] Red-team: prompt tries to skip approval → denied

## Forbidden

- Prompt-only enforcement of money/legal controls
- Client-only "confirm" without server-side approval record
- Logging chain-of-thought as audit evidence
