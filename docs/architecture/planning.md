# Planning

## Mode for MVP

**Graph + bounded model nodes** (not unbounded adaptive loop).

| Step | Node | Effect |
|---|---|---|
| Intake / classify | Planner | read |
| Credit assessment | Credit | read |
| Legal review | Legal | read |
| Ops action / draft | Operations | write_reversible |
| Synthesize | Planner | read |

## Plan contract

Each plan needs: goal, preconditions, state schema, steps, transitions,
allowed tools, budgets, checkpoints, terminal states, retry, compensation.
Persist plan version/hash with the run.

## Invariants

- Finite `max_steps`, deadline, budgets, recursion limit
- Model outputs schema-validated before transitions
- Pause/resume does not replay side effects (idempotency)
- Re-plan only inside allowed boundary; risk increase → escalate
- Terminal: `completed` | `failed` | `cancelled` | `expired`

Part harness: [`../harness/parts/orchestration.md`](../harness/parts/orchestration.md).
