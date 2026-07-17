# Feature Intake

Every implementation prompt enters intake before code changes. The Digital
Expert Agents problem statement also entered through this gate as a `new_spec`.

## Intake flow

```text
User prompt / problem statement
    |
    v
Classify input type
    |
    v
Restate as work item
    |
    v
Find affected product docs, part harnesses, stories
    |
    v
Run risk checklist
    |
    v
Choose lane: tiny | normal | high-risk
```

## Input types

| Type | Use when | Typical artifact |
|---|---|---|
| New spec | Turning problem statement into harness-ready docs | Product docs, epics |
| Spec slice | Implementing selected behavior from accepted product | Story packet |
| Change request | Changing accepted behavior | Story or patch |
| New initiative | Adding a larger product area | Epic + stories |
| Maintenance | Deps, infra, operational behavior | Story / decision |
| Harness improvement | Improving collaboration / proof | Docs or backlog |

## Work item breakdown

```text
spec -> epic -> story or spike -> task
```

- `spec`: Digital Expert Agents (this challenge)
- `epic`: coherent outcome (e.g. multi-agent credit-limit demo)
- `story`: behavior change with acceptance criteria
- `spike`: timeboxed research → decision
- `task`: small execution step under one story

Do not generate all tasks up front. Create tasks only after a story is selected.

## Risk checklist (banking + agents)

Escalate to **high-risk** if any apply:

- [ ] Auth, sessions, service tokens, or RBAC
- [ ] Money-moving or irreversible external side effects
- [ ] Agent write tools or HITL policy changes
- [ ] Cross-tenant data / knowledge isolation
- [ ] Prompt / tool surface that can escalate privileges
- [ ] Architecture boundary change (ports, public contracts)
- [ ] Audit / observability contract change

## Mapping to parts

After intake, tag the affected parts so agents load the right harness:

| Signal in request | Part(s) |
|---|---|
| planner, decompose, assign, LangGraph | orchestration |
| Credit / Legal / Ops agent behavior | specialist-agents |
| tool call, function calling, API action | tools |
| RAG, knowledge, embeddings, corpus | rag |
| `/v1/agent`, NestJS bridge, draft transfer | agent-bridge |
| dashboard, traces, collaboration graph | dashboard |
| single vs multi, latency, comparison | benchmark |
| approval, guardrail, kill switch | security-hitl |

## Intake record template

```yaml
intake:
  type: spec_slice | change_request | ...
  summary: "<one sentence>"
  lane: tiny | normal | high-risk
  parts: [orchestration, tools, ...]
  in_scope: []
  out_of_scope: []
  related_stories: []
  proof_expected: []
```
