# Demo runbook

## Preconditions

- Compose stack up (web, api, agent-api, worker, postgres, redis)
- Seed loaded (`data/seed`)
- Corpora ingested
- LLM API key configured

## Script (5–7 min)

1. Open dashboard; show empty state briefly
2. Paste demo scenario request (VI)
3. Show live timeline + collaboration graph as specialists run
4. Expand tool inspector on one Credit + one Legal call
5. If HITL enabled: approve Ops draft
6. Toggle single-agent mode; re-run BC-05; show comparison table
7. Point to audit/correlation ids

## Failure fallback

- Pre-recorded trace JSON for BC-05 if live LLM unavailable
- Still show architecture + harness docs
