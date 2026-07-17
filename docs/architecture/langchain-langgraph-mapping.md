# LangChain / LangGraph mapping

Architecture is runtime-neutral. LangGraph is the MVP adapter for planner
graph, checkpoints, and HITL interrupt/resume.

| Capability | Mapping | Boundary |
|---|---|---|
| Adaptive loop | LangChain agent | Budgets; canonical output |
| Typed tool | LangChain tool + schema | Dispatcher still authorizes |
| Deterministic workflow | LangGraph state graph | Transitions in testable code |
| Working state | LangGraph checkpoint | Not durable business memory |
| HITL | Interrupt + resume | Approval record owned by platform |
| Streaming | Graph stream → canonical events | Channel adapter at agent-api |

## Ports

`ChatRuntime`, `WorkflowRuntime`, `CheckpointStore`, `MemoryStore`,
`ToolRegistry/Dispatcher`.

Part harness: [`../harness/parts/orchestration.md`](../harness/parts/orchestration.md).
