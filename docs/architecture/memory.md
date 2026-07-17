# Memory & RAG

| Type | Content | SoR |
|---|---|---|
| Working state | Step, intermediates, retries | Runtime checkpoint |
| Conversation | Messages, citations, tool summaries | Platform |
| Semantic memory | Verified facts/preferences | Platform (opt-in) |
| Episodic | Prior actions/results | Audit/platform |
| Domain knowledge | Policies, SOPs, regulations | Domain + knowledge module |

Checkpoint ≠ long-term memory. Vector index ≠ source of truth.

## RAG read path

1. Hard filter tenant / domain / classification
2. Top-k with budget; rerank; drop stale duplicates
3. Attach provenance + freshness
4. Treat retrieved text as untrusted (anti-injection)
5. Record memory ids used

Part harness: [`../harness/parts/rag.md`](../harness/parts/rag.md).
