# Part harness — Specialist agents

## Purpose

Three digital experts: Credit, Legal/Compliance, Operations. Each has a narrow
purpose, tool allowlist, domain RAG, and agent contract.

## Code homes

- `modules/credit/`, `modules/legal/`, `modules/operations/`
- `config/agents/*.yaml`
- `config/prompts/{credit,legal,operations}/`

## Agents (locked for MVP)

| Agent id | Purpose | Default write policy |
|---|---|---|
| `credit-expert` | Creditworthiness, DTI, loan history | deny |
| `legal-compliance` | Regulation, AML/compliance flags | deny |
| `operations-expert` | Account status, service-request drafts | require_approval |

## In scope

- Agent contract YAML filled and reviewed
- Specialist subgraph / node with allowlisted tools
- Domain RAG tool scoped to that agent's corpus
- Structured result with citations / evidence refs

## Out of scope

- Planner decomposition (orchestration part)
- Cross-domain knowledge without routing through planner
- Executing irreversible banking actions

## Intake signals

`credit agent`, `legal agent`, `ops agent`, `specialist`, `digital expert`

## Default lane

- New agent / risk_tier change → **high-risk**
- Prompt or RAG query tuning → **normal**
- Contract copy edits → **tiny**

## Context to read

1. This file
2. Matching `config/agents/<id>.yaml`
3. `docs/architecture/overview.md`
4. Domain module README under `modules/<domain>/`
5. Current story packet

## Proof checklist

- [ ] Agent contract exists and matches runtime allowlist
- [ ] Agent cannot call tools outside allowlist
- [ ] Answers that cite numbers come from tools, not free text invention
- [ ] RAG hits are domain-scoped (credit ≠ legal corpus)
- [ ] Events carry `agent_id` + `agent_version`

## Forbidden

- Sharing one mega-prompt with all tools "for convenience"
- Letting a specialist re-plan global scope
- Embedding secrets or full PAN in prompts/memory
