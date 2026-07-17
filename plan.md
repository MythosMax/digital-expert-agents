# Plan — Digital Expert Agents

Kế hoạch triển khai monorepo `digital-expert-agents` cho Hack CX Together 2026
(SHB): đội AI chuyên gia ngân hàng (Credit, Legal/Compliance, Operations) với
planner, tool use, RAG, HITL, dashboard traces, và so sánh single vs multi-agent.

> Docs SoT: [`docs/product/`](docs/product/), [`docs/harness/`](docs/harness/),
> [`docs/architecture/implementation-roadmap.md`](docs/architecture/implementation-roadmap.md).
> Stories: [`docs/stories/backlog.md`](docs/stories/backlog.md).

---

## 1. Mục tiêu hackathon (locked)

| # | Deliverable | Done khi |
|---|---|---|
| 1 | ≥3 specialists cộng tác 1 request phức tạp | Demo CIF-12345 tăng hạn mức SME chạy E2E |
| 2 | Planner decompose + assign | Plan JSON schema-valid, ≥3 tasks |
| 3 | Tool use thực tế | Mỗi specialist ≥1 tool call (không chỉ text) |
| 4 | Dashboard traces | Timeline + collaboration graph + task board |
| 5 | Single vs multi comparison | ≥5 cases, bảng latency/tokens/success/unsafe |

**Không làm (MVP):** thanh toán agent-execute, core banking thật, K8s, unbounded loop.

---

## 2. Kiến trúc chốt

```text
apps/web (Next.js) ──SSE──► apps/agent-api (FastAPI)
       │                         │
       │                         ▼
       │                   apps/agent-worker (LangGraph)
       │                         │
       │              Planner → Credit / Legal / Ops
       │                         │
       └──HTTP──► apps/api (NestJS) ◄── /v1/agent/* (scoped JWT)
                         │
                    PostgreSQL + Redis + pgvector
```

| Quyết định | Choice | Lý do |
|---|---|---|
| Runtime | LangGraph supervisor | Checkpoint, HITL interrupt, state graph |
| Banking API | NestJS + agent-bridge | Scoped JWT, draft-only writes |
| Frontend | Next.js | Dashboard + chat + design system |
| Vector | pgvector (cùng Postgres) | Ít infra cho demo |
| Observe | Canonical events + (optional) Langfuse | Trace cho judges |
| Agent → API auth | Scoped service JWT | Không dùng user cookie |

Chi tiết: [`STRUCTURE.md`](STRUCTURE.md), [`docs/architecture/ARCHITECTURE.md`](docs/architecture/ARCHITECTURE.md).

---

## 3. Demo scenario chính

> Khách hàng Nguyễn Văn A (CIF-12345) yêu cầu tăng hạn mức tín dụng từ
> 500 triệu lên 1 tỷ VND cho khoản vay SME. Đánh giá khả năng duyệt và lập
> kế hoạch xử lý.

Luồng: Planner → Credit (score/DTI/policy) → Legal (regulation/AML) →
Ops (status + draft, HITL) → Synthesize → Dashboard.

Baseline: cùng request, mode `single` (1 agent, union tools).

---

## 4. Phased plan

### Phase 0 — Baseline (đã có phần lớn trong repo docs)

- [x] Product contract, agent contracts YAML, harness parts
- [x] Epics + backlog US-001…013
- [ ] Chốt LLM provider + API key process
- [ ] `git commit` initial scaffold (khi team sẵn sàng)

**Exit:** boundaries + prohibited actions được team acknowledge.

### Phase 1 — Tracer bullet (EPIC-01) — MVP tối thiểu

Stories: US-001 → US-005

| Thứ tự | Việc | Owner gợi ý | Proof |
|---|---|---|---|
| 1 | Scaffold monorepo (pnpm/turbo + Python agent apps) | Platform | Apps boot |
| 2 | Nest: scoped token + `GET /v1/agent/accounts` (+ credit summary) | Backend | Cookie rejected; Bearer OK |
| 3 | Seed CIF-12345 + Credit read tools | Backend/AI | Tool trả số từ fixture |
| 4 | agent-api: `POST /runs` + SSE canonical events | AI | Events stream |
| 5 | Dashboard timeline v1 | Frontend | 1 run hiện timeline |

**Exit:** Credit agent trả lời 1 câu credit có provenance; không cross-tenant leak.

Part harness: `agent-bridge`, `specialist-agents`, `tools`, `dashboard`.

### Phase 2 — Multi-agent + RAG (EPIC-02) — Demo cốt lõi

Stories: US-006 → US-009

| Thứ tự | Việc | Proof |
|---|---|---|
| 1 | LangGraph supervisor (planner + 3 nodes + synthesize) | ≥3 tasks cho demo request |
| 2 | Legal + Ops specialists + allowlists | Contract YAML = runtime allowlist |
| 3 | Ingest 3 corpora (`data/knowledge/*`) | Domain filter: credit ↛ legal chunks |
| 4 | Collaboration graph + task board | UI hiện planner ↔ specialists |

**Exit:** Demo scenario E2E; crash/resume không double side effect (read-only OK).

Part harness: `orchestration`, `rag`, `dashboard`.

### Phase 3 — Write + HITL (EPIC-03) — Điểm khác chatbot

Stories: US-010 → US-011

| Thứ tự | Việc | Proof |
|---|---|---|
| 1 | `create_service_request_draft` + idempotency | Draft tạo; không execute limit change |
| 2 | LangGraph interrupt + approval record | Approve/reject/expire đúng semantics |
| 3 | Approval queue UI | Human quyết định trên dashboard |
| 4 | Red-team: prompt skip approval | Denied + audited |

**Exit:** unsafe unapproved write = 0; audit reconstruct được.

Part harness: `security-hitl`, `tools`.

### Phase 4 — Benchmark + polish (EPIC-04) — Pitch

Stories: US-012 → US-013

| Thứ tự | Việc | Proof |
|---|---|---|
| 1 | Mode `single` \| `multi` + ≥5 cases | Bảng metrics |
| 2 | Docker Compose one-command | Runbook chạy được |
| 3 | EN/VI labels core UI | Switch locale |
| 4 | Demo rehearsal theo `docs/demo/runbook.md` | 5–7 phút ổn định |

**Exit:** Judges chạy / xem demo + comparison mà không cần giải thích nội bộ.

---

## 5. Lịch gợi ý (5 ngày hackathon)

| Ngày | Focus | Must-ship |
|---|---|---|
| D1 | Phase 0–1 | Bridge + 1 Credit tool + SSE + timeline |
| D2 | Phase 2 start | Supervisor graph + 3 agents wire |
| D3 | Phase 2 finish | RAG + collaboration UI + demo E2E |
| D4 | Phase 3 | HITL draft + approval UI |
| D5 | Phase 4 | Benchmark, compose, rehearsal |

Nếu trễ: **cắt Phase 3 trước khi cắt Phase 2**. Dashboard collaboration quan trọng hơn HITL; HITL quan trọng hơn benchmark đẹp.

---

## 6. Phân công gợi ý (4–5 người)

| Role | Phase chính | Surfaces |
|---|---|---|
| Agent / AI | 1–2, 4 | LangGraph, prompts, RAG, benchmark |
| Backend | 1, 3 | Nest, bridge, seed, draft APIs |
| Frontend | 2, 4 | Chat, timeline, graph, approval, compare |
| Platform | 0, 4 | Compose, env, observe, harness |
| Product / Demo | 0, 4 | Scenario, corpus text, pitch script |

Conductor (coding): 1 người giữ intake → proof → trace theo [`docs/harness/HARNESS.md`](docs/harness/HARNESS.md).

---

## 7. Definition of Done (hackathon)

- [ ] 3 specialists + planner trên 1 complex request
- [ ] Mỗi specialist: ≥1 tool + ≥1 RAG citation (policy claims)
- [ ] Dashboard: timeline + graph + task status
- [ ] ≥1 write draft với HITL (hoặc documented fallback nếu cắt Phase 3)
- [ ] Single vs multi: ≥5 cases, unsafe rate = 0
- [ ] Compose demo + runbook
- [ ] Agent contracts trong `config/agents/` khớp runtime allowlist
- [ ] Không agent token nào execute transfer / money move

---

## 8. Rủi ro & mitigation

| Rủi ro | Mitigation |
|---|---|
| Scaffold chậm | Bám STRUCTURE.md + vertical slice sớm; tránh dựng full stack trước demo |
| LLM flaky lúc demo | Fallback trace JSON cho BC-05; cache 1 happy-path run |
| Hallucinate số liệu | Số chỉ từ tools; RAG chỉ policy text + citation |
| Scope creep domain | Chỉ CIF-12345 + limit-increase; không build full loan OS |
| Architecture drift | `STRUCTURE.md` + part harness là SoT; không invent layer mới |

---

## 9. Cách làm việc hàng ngày

```text
intake (lane + parts)
  → chọn 1 story từ backlog
  → đọc docs/harness/parts/<part>.md
  → implement bounded slice
  → proof theo TEST_MATRIX
  → update story status + trace notes
```

Trước khi claim done: checklist trong part harness tương ứng.

---

## 10. Next actions (ngay)

1. Commit scaffold docs (nếu chưa) — chỉ khi được yêu cầu.
2. Bắt đầu **US-001** scaffold monorepo runnable.
3. Song song: viết seed SQL/JSON cho CIF-12345 + 5–10 doc/corpus.
4. Chốt model (GPT-4o / Claude) và `.env.example`.

---

## 11. Liên kết nhanh

| Cần | Mở |
|---|---|
| Product | [`docs/product/README.md`](docs/product/README.md) |
| Demo script | [`docs/demo/runbook.md`](docs/demo/runbook.md) |
| Part harness | [`docs/harness/parts/`](docs/harness/parts/) |
| Test proof | [`docs/harness/TEST_MATRIX.md`](docs/harness/TEST_MATRIX.md) |
| Stories | [`docs/stories/`](docs/stories/) |
| Agent YAML | [`config/agents/`](config/agents/) |
