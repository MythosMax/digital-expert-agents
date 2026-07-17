# Claude Code entry

Import project rules from [`AGENTS.md`](AGENTS.md).

Additional Claude-specific notes:

1. Prefer vertical slices (schema → API → agent tool → UI) over half-built layers.
2. When implementing agents, fill `config/agents/*.yaml` and
   `templates/tool-spec.template.yaml` instances first.
3. Never widen `/v1/agent/*` by handing agents a general-purpose user token.
4. For multi-agent work: conductor owns planning; sub-agents own one task each.
5. Leave the tree dirty for the human to commit unless asked to commit.

Harness: `docs/harness/HARNESS.md`.
