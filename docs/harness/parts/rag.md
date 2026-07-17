# Part harness — RAG / Knowledge

## Purpose

Domain-specific retrieval for each specialist. Domain records are source of
truth; vector index is a projection.

## Code homes

- `modules/knowledge/`
- `packages/shared-retrieval/`, `packages/shared-embeddings/`
- `data/knowledge/{credit,legal,operations}/`
- `config/knowledge/`

## Corpora (MVP)

| Corpus | Consumer agent | Content examples |
|---|---|---|
| `credit` | credit-expert | Credit policy, scoring rules, DTI guidelines |
| `legal` | legal-compliance | NHNN/regulatory summaries, AML checklist |
| `operations` | operations-expert | SOPs, branch handoff, service-request SOP |

## In scope

- Ingest → chunk → embed → index per tenant+domain
- Hard filters before semantic rank (tenant, domain, classification)
- Citations / provenance on retrieved chunks
- Prompt-injection resistance (retrieved text is not trusted instruction)

## Out of scope

- Treating vector hits as authoritative numbers (use tools for scores/balances)
- Cross-domain bleed without explicit planner routing
- Long-term personal memory without consent policy

## Intake signals

`RAG`, `knowledge`, `embedding`, `corpus`, `citation`, `pgvector`

## Default lane

- Isolation / retention / deletion policy → **high-risk**
- Adding docs to corpus / chunk params → **normal**
- Sample doc copyedits → **tiny**

## Context to read

1. This file
2. `docs/architecture/memory.md`
3. `modules/knowledge/README.md`
4. Corpus README under `data/knowledge/<domain>/`

## Proof checklist

- [ ] Query from Credit agent cannot return Legal-only chunks
- [ ] Each cited claim in demo has a provenance id
- [ ] Stale / deleted source no longer retrieved (or marked tombstoned)
- [ ] No secrets embedded in index
- [ ] Events: `memory.read` with memory ids used

## Forbidden

- One shared undifferentiated index for all agents in production mode
- Putting business calculation rules only inside PDFs without code/tools
- Logging full document PII in traces
