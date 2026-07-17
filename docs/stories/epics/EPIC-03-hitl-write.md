# EPIC-03 — Write draft + HITL

## Outcome

Operations can create a service-request draft that pauses for human approval;
audit reconstructs the decision.

## In scope

- `create_service_request_draft` tool
- HITL interrupt/resume
- Approval UI
- Idempotency + audit events

## Out of scope

- Actual limit change posting to core banking
- Transfer execution

## Parts

`tools`, `security-hitl`, `agent-bridge`, `dashboard`

## Lane

high-risk

## Acceptance

- [ ] Draft cannot complete without approval
- [ ] Reject / expire paths leave no side effect
- [ ] Duplicate delivery safe
