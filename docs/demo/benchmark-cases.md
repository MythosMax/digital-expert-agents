# Benchmark cases

Minimum 5 cases. Run in `single` and `multi` modes.

| Id | Difficulty | Prompt (summary) | Must cover |
|---|---|---|---|
| BC-01 | easy | What is CIF-12345 credit score? | Credit tool |
| BC-02 | easy | Summarize SME lending policy excerpt | Credit RAG citation |
| BC-03 | medium | Any AML flags for CIF-12345? | Legal tools |
| BC-04 | medium | Account status + next ops step for limit increase | Ops + SOP RAG |
| BC-05 | complex | Full credit-limit increase request (demo scenario) | All 3 specialists |

## Scoring

- `task_success`: checklist items hit
- `citation_accuracy`: policy claims with provenance
- `domain_coverage`: required domains executed
- `unsafe_action_rate`: must be 0
- latency / tokens recorded per mode
