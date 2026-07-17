# Context Engineering Rules

Put the right information in the model for the current phase and risk lane.
Do not maximize context.

## Stable always-read list

- `AGENTS.md`
- Matching `docs/harness/parts/<part>.md` for affected parts
- Current story packet (if any)

## Phases

### Intake

| Source | Tiny | Normal | High-risk |
|---|---|---|---|
| `AGENTS.md` | Must | Must | Must |
| `docs/harness/FEATURE_INTAKE.md` | Must | Must | Must |
| `docs/product/README.md` | Should | Must | Must |
| `docs/harness/parts/*` (affected) | Should | Must | Must |
| `docs/architecture/ARCHITECTURE.md` | Skip | Should | Must |

### Planning

| Source | Tiny | Normal | High-risk |
|---|---|---|---|
| Files to edit | Must | Must | Must |
| Part harness | Should | Must | Must |
| `docs/templates/story.md` | Skip | Must when creating story | Should |
| `docs/templates/high-risk-story/*` | Skip | Skip unless escalates | Must |
| Agent contracts in `config/agents/` | Skip | Must if agent behavior | Must |
| Tool specs / policies | Skip | Must if tools/HITL | Must |

### Implementation

| Source | Tiny | Normal | High-risk |
|---|---|---|---|
| Files being changed | Must | Must | Must |
| Adjacent same-pattern files | Should | Must | Must |
| Product docs for behavior | Skip if copy-only | Must | Must |
| Unrelated parts / historical traces | Skip | Skip | Should only if decision-relevant |

### Validation

| Source | Tiny | Normal | High-risk |
|---|---|---|---|
| Story acceptance criteria | Should | Must | Must |
| `docs/harness/TEST_MATRIX.md` | Should | Must | Must |
| Part-specific proof checklist | Should | Must | Must |
| Benchmark protocol (if touched) | Skip | Skip unless requested | Must |

### Trace

| Source | Tiny | Normal | High-risk |
|---|---|---|---|
| `docs/harness/TRACE_SPEC.md` | Should | Must | Must |
| `git status --short` | Must | Must | Must |
| Validation output | Should | Must | Must |

## Stop rules

- Stop reading when the next file would not change the plan or proof.
- Prefer the part harness over re-reading the full architecture set.
- Prefer the current story packet over inventing scope.
