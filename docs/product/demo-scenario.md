# Demo scenario (primary)

## Request

> Khách hàng Nguyễn Văn A (CIF-12345) yêu cầu tăng hạn mức tín dụng từ
> 500 triệu lên 1 tỷ VND cho khoản vay SME. Hãy đánh giá khả năng duyệt và
> lập kế hoạch xử lý.

## Expected multi-agent flow

1. **Planner** — classify + create ≥3 tasks
2. **Credit** — DTI / score / loan history + credit policy RAG → recommendation
3. **Legal** — regulatory/AML/compliance flags + legal corpus RAG
4. **Operations** — account status + draft service request (HITL if write)
5. **Planner** — synthesize with citations and next steps
6. **Dashboard** — show task tree, collaboration, tool calls, timing

## Fixtures required

- Customer CIF-12345
- Existing SME loan @ 500M VND
- Credit score + repayment history
- Sample NHNN/internal policy docs in each corpus
- Branch / ops SOP for limit-increase handling

## Single-agent baseline

Same request, one agent with union of tools/corpora, no decomposition.
Record latency, tokens, success, citation accuracy, domain coverage.
