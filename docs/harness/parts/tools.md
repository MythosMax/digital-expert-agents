# Part harness — Tools

## Purpose

Practical tool use: agents call APIs, query data, or create drafts — not only
generate text. Dispatcher is the security boundary.

## Code homes

- `modules/*/agent-tools/`
- `packages/governance/`
- `templates/tool-spec.template.yaml` → filled specs under `config/policies/tools/`
- NestJS targets via agent-bridge (`apps/api`)

## Effect classes

| Effect | Examples | Default control |
|---|---|---|
| `read` | credit score, account status, search KB | permission + log |
| `write_reversible` | service-request draft | approval by risk + idempotency |
| `write_irreversible` | send external notice, payment | explicit approval + narrow scope |
| `external_execution` | browser/shell | sandbox + approval (out of MVP) |

## In scope

- Typed ToolSpec (input/output schema, version, permissions)
- Dispatcher: allowlist → validate → permission → budget → execute
- Idempotency keys for writes
- Redacted structured results back to model

## Out of scope

- Arbitrary function names from model output
- Direct DB writes from agent worker
- Transfer **execution** (human MFA path only)

## Intake signals

`tool`, `function calling`, `dispatcher`, `create draft`, `API action`

## Default lane

- New write tool / effect class change → **high-risk**
- New read tool within existing permissions → **normal**
- Description copy → **tiny**

## Context to read

1. This file
2. `docs/architecture/tool-orchestration.md`
3. `docs/harness/parts/agent-bridge.md`
4. `docs/harness/parts/security-hitl.md` (if write)
5. Tool spec YAML for the tool being changed

## Proof checklist

- [ ] ToolSpec filled before registration
- [ ] Schema validation rejects invalid input
- [ ] Domain callee re-checks ownership/tenant
- [ ] Write tools emit `tool.proposed` → (approval) → `tool.started/succeeded|failed`
- [ ] Duplicate delivery does not double-apply write
- [ ] Demo uses ≥1 real tool call per specialist

## Forbidden

- Authorization only in tool description text
- Returning raw secrets to the model
- Retrying uncertain writes without reconciliation
