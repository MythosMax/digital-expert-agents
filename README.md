# Digital Expert Agents

Multi-agent AI system for banking operations (Hack CX Together 2026 / SHB).
Each agent acts as a digital specialist (Credit, Legal/Compliance, Operations),
plans tasks, uses tools, retrieves domain knowledge via RAG, collaborates, and
executes bounded actions — not only text answers.

## Entrypoints

| File | Who reads it |
|---|---|
| [`AGENTS.md`](AGENTS.md) | Every coding agent |
| [`CLAUDE.md`](CLAUDE.md) | Claude Code (harness shim) |
| [`STRUCTURE.md`](STRUCTURE.md) | Ownership tree |
| [`docs/architecture/index.md`](docs/architecture/index.md) | Architecture set |
| [`docs/harness/HARNESS.md`](docs/harness/HARNESS.md) | Change operating model |
| [`docs/product/README.md`](docs/product/README.md) | Product contract |
| [`plan.md`](plan.md) | Implementation plan (phases, DoD, schedule) |

## Layout

```text
apps/                 # web, api, agent-api, agent-worker, composition
packages/             # kernel, runtime, governance, shared-*
modules/              # credit, legal, operations, knowledge, identity
config/               # agent contracts, prompts, policies
data/                 # seed data + knowledge corpora
docs/                 # architecture, harness, product, stories, demo
templates/            # architecture form templates (YAML/MD)
scripts/              # harness schema + CLI hooks
infra/                # docker-compose / UAT
```

## Harness (change control)

Material changes go through intake → work item → proof → trace.

```bash
# When harness-cli is installed:
scripts/bin/harness-cli init && scripts/bin/harness-cli migrate
scripts/bin/harness-cli query matrix
scripts/bin/harness-cli intake --type new_spec --summary "Digital Expert Agents MVP" --lane high-risk
```

See [`docs/harness/`](docs/harness/).

## Hackathon deliverables (locked)

1. Working demo with ≥ 3 specialists (Credit, Legal, Operations) on one complex request
2. Planner decomposes work and assigns executor agents
3. Practical tool use (APIs / data / drafts — not text-only)
4. Dashboard: agent traces, task status, decisions, collaboration flows
5. Performance comparison: single-agent chatbot vs multi-agent system

## Status

Docs + filesystem skeleton only. Application source lands after kickoff /
implementation stories are selected. See
[`docs/architecture/implementation-roadmap.md`](docs/architecture/implementation-roadmap.md).
