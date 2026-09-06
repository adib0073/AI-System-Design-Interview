# Engineering Blogs & Papers — Chapter 18 (Deep Research & Planning Agent)

Curated, interview-relevant reading. Focus on *orchestration, transactions, and durable state*, not demos. Search titles if links move.

> **Living note:** deep-research and agent products are the fastest-moving area in the book — treat all product entries as directional.

## Start here (highest signal)
- **Anthropic "How we built our multi-agent research system"** — the reference for **orchestrator + parallel sub-agents**, including honest discussion of token-cost trade-offs and when multi-agent is (and isn't) worth it. Read first.
- **Anthropic "Building effective agents"** — the plan/tool/verify philosophy and "keep it as simple as the task allows."
- **OpenAI Deep Research** and **Google Gemini Deep Research** — the canonical deep-research pattern (decompose → browse many sources → synthesize a cited report).

## Grounding, citations & faithfulness
- **Perplexity** engineering/product write-ups — grounded, cited answers; source attribution.
- **RAGAS / faithfulness metrics** — evaluating whether synthesis is supported by sources (shared with Ch. 6/13).

## Transactions & reliability (the money path)
- **Saga pattern** (Garcia-Molina & Salem, 1987; Chris Richardson's microservices.io) — compensating transactions for multi-step, cross-service operations. The key transactional reference.
- **Idempotency** design guides (Stripe's idempotency-keys docs) — safe retries for money actions.
- **Durable execution / workflow engines** — Temporal, AWS Step Functions, Azure Durable Functions — checkpointing and resumable long-running workflows.

## Computer-use & action-taking agents
- **OpenAI Operator / Computer-Using Agent** — agents taking real web actions (incl. bookings); consent and transaction challenges.
- **AutoGPT / BabyAGI (historical)** — early autonomous agents; study the failure modes (looping, cost blowup, no grounding) this chapter's disciplines fix.

## Evaluation
- **GAIA** and deep-research/agent benchmarks — evaluating open-ended, multi-step tasks.
- **LLM-as-a-judge** + trace-based evaluation references — scoring plan quality and process, not just the final answer.

## How to use in prep
1. Read Anthropic's multi-agent research post — it anchors orchestrator/sub-agents and the cost trade-off.
2. Learn the **saga/compensation + idempotency** pattern well enough to answer "flight books, hotel fails."
3. Have the **plan-vs-execute + human approval gate** principle ready.
4. Prepare the **durable orchestration / checkpointing** answer for "the server restarts mid-task."
