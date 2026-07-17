# Part harness — Orchestration / Planner

## Purpose

Planner (supervisor) decomposes a banking request into bounded tasks and
assigns them to specialist executor agents. Implemented as a LangGraph state
graph with finite budgets.

## Code homes

- `packages/runtime-langgraph/`
- `packages/agent-kernel/{contracts,application,ports}/`
- `apps/agent-worker/`
- `config/prompts/planner/`
- `templates/workflow-plan.template.yaml` → filled under `config/policies/`

## In scope

- Task decomposition with schema-validated plan JSON
- Conditional routing to Credit / Legal / Operations
- Synthesis node that merges specialist results with evidence
- Max steps, wall-clock timeout, token/cost budget
- Durable checkpoint for crash/resume

## Out of scope

- Domain business rules (live in modules)
- Direct NestJS DB access
- Unbounded adaptive loops without budgets

## Intake signals

`planner`, `decompose`, `supervisor`, `LangGraph`, `assign tasks`, `orchestration`

## Default lane

- Graph topology / plan schema change → **high-risk**
- Prompt tuning within accepted schema → **normal**
- Doc-only → **tiny**

## Context to read

1. This file
2. `docs/architecture/planning.md`
3. `docs/architecture/langchain-langgraph-mapping.md`
4. `docs/product/demo-scenario.md`
5. Current story packet

## Proof checklist

- [ ] Plan output validates against schema
- [ ] Every plan step has assignee + allowed tools
- [ ] Budgets enforced (steps / timeout)
- [ ] Crash/resume does not duplicate side effects
- [ ] Canonical events: `run.started`, `plan.created`, `run.completed|failed`
- [ ] Complex demo request produces ≥3 specialist tasks

## Forbidden

- Putting authorization only in the planner prompt
- Exposing LangGraph node/checkpoint IDs in public product APIs
- Re-planning that expands risk without escalation
