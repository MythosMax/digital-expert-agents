# Tool orchestration

Model may propose a tool call; dispatcher decides whether it runs.

## Dispatch flow

1. Resolve tool from agent allowlist + version
2. Validate input schema / size
3. Re-check tenant, permission, resource scope
4. Apply effect/risk policy, rate limit, timeout, approval
5. Create idempotency key; execute via public surface
6. Sanitize output; structured result only
7. Emit lifecycle/audit events

Part harness: [`../harness/parts/tools.md`](../harness/parts/tools.md).
