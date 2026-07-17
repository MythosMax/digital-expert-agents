# Harness audit

Periodic checks that docs, stories, and proof stay aligned.

## Checklist

- [ ] Every epic in `docs/stories/epics/` maps to product outcomes in `docs/product/`
- [ ] Every in-progress story names affected parts and proof
- [ ] Agent contracts in `config/agents/` match specialist-agents part harness
- [ ] TEST_MATRIX surfaces have at least one story covering them for MVP
- [ ] No high-risk story marked done without Detailed-tier trace notes
- [ ] Benchmark cases ≥5 documented
- [ ] Forbidden items in part harnesses still hold in implementation plans

## Drift signals

- Code home paths in part harnesses that do not exist in STRUCTURE.md
- Tools referenced in prompts but missing ToolSpec
- Dashboard panels promised in product docs but absent from stories
- Write tools without HITL policy reference
