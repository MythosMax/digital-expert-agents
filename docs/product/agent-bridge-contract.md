# Product — Agent bridge contract

## Auth

Short-lived scoped JWT: `sub`, `scope[]`, `conversationId`, `exp`.
Presented as `Authorization: Bearer` on `/v1/agent/*` only.

## MVP surface

- `GET /v1/agent/accounts`
- `GET /v1/agent/transactions`
- `GET /v1/agent/credit/summary` (demo)
- `GET /v1/agent/compliance/flags` (demo)
- `POST /v1/agent/service-requests/draft`
- `POST /v1/agent/transfers/draft`

Agents never execute transfers. Correlation: `conversationId` + `traceId`.

Aligned with sibling `web-template` AI-agent contract.
