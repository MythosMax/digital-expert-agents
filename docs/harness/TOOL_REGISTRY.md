# Tool registry (project)

Machine-oriented list of tools coding agents and harness may use. Product
agent tools are registered separately via ToolSpec YAML.

## Harness / repo tools (planned)

| Name | Responsibility | Purpose |
|---|---|---|
| `harness-cli` | Task state | Intake, stories, traces, eval |
| `check-architecture-policy` | Architecture gate | Import boundary fixtures |
| `demo-seed` | Verification | Load mock SHB fixtures |
| `benchmark-run` | Verification | Single vs multi case runner |
| `rag-ingest` | Verification | Rebuild domain corpora indexes |

Register external commands when CLI is available:

```bash
scripts/bin/harness-cli tool register \
  --name benchmark-run \
  --command ./scripts/benchmark-run.sh \
  --description "Run single vs multi-agent benchmark cases" \
  --responsibility Verification \
  --args "mode:enum:required:single,multi,both"
```

## Product agent tools (MVP allowlists)

See part harness [`parts/tools.md`](parts/tools.md) and:

- `config/agents/credit-expert.yaml`
- `config/agents/legal-compliance.yaml`
- `config/agents/operations-expert.yaml`
