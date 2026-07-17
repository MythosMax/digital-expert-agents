# Improvement protocol

How harness itself evolves without silent drift.

```text
friction in trace OR verifier failure
  -> failure attribution (category + signature)
  -> proposal (what to change in docs/templates/tests)
  -> held-in eval (known cases still pass)
  -> held-out eval (at least one new/related case)
  -> promote OR reject with reason
```

## Rules

1. Do not change intake/trace/proof rules mid-story without a proposal note.
2. Promoted changes must update the relevant part harness in the same PR/change.
3. If a product bug is mislabeled as harness friction, fix the product story instead.
4. Prefer smaller harness deltas that unblock the next coding agent.
