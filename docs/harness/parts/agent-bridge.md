# Part harness — Agent bridge / Banking API

## Purpose

Stable contract between agent runtime and NestJS banking backend. Agents act
with scoped service tokens on `/v1/agent/*` — never user HttpOnly cookies.

## Code homes

- `apps/api/` (NestJS modules + `integrations/agent-bridge`)
- `packages/contracts/`
- Sibling reference: `../web-template/integrations/2026-07-16 - ai-agent-contract.md`

## MVP endpoints

| Endpoint | Purpose | Can move money? |
|---|---|---|
| `GET /v1/agent/accounts` | Account summaries for scoped user | No |
| `GET /v1/agent/transactions` | Transaction history | No |
| `GET /v1/agent/credit/*` | Credit score / DTI / loan history (demo) | No |
| `GET /v1/agent/compliance/*` | Compliance flags (demo) | No |
| `POST /v1/agent/service-requests/draft` | Draft ops request | No |
| `POST /v1/agent/transfers/draft` | Draft transfer proposal | No |

Transfer **execution** remains human MFA `POST /v1/transfers`.

## In scope

- Mint short-lived scoped JWT per conversation
- Ownership checks identical to human routes
- Independent rate limit for agent namespace
- `conversationId` + `traceId` correlation

## Out of scope

- Giving agents a user session cookie
- Widening scope via general-purpose user token
- Agent-side memory persistence inside NestJS

## Intake signals

`agent-bridge`, `/v1/agent`, NestJS, service token, draft transfer

## Default lane

- New agent endpoint / token scope → **high-risk**
- Read DTO field add → **normal**
- Spec wording → **tiny**

## Context to read

1. This file
2. `docs/product/agent-bridge-contract.md`
3. `docs/architecture/security-deployment.md`
4. `docs/harness/parts/security-hitl.md`

## Proof checklist

- [ ] Bearer token required; cookie auth rejected on `/v1/agent/*`
- [ ] Token cannot call transfer execute
- [ ] Cross-user resource access returns 403/404 per policy
- [ ] Rate limit independent of human routes
- [ ] Audit log includes `conversationId` and `traceId`

## Forbidden

- Executing money movement from agent token
- Logging full tokens or secrets
