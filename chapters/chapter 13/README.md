# Chapter 13 — Agentic Customer Support

Companion resources for Chapter 13, the first of the book's three agentic case studies (with Ch. 17 and 18). It applies the Chapter 7 agent toolkit to a real product, and its signature idea is the **read/write tool split** with **approval gates on money actions**.

Chapter 13 covers LLM agents, the ReAct pattern, tool use (read vs. write), RAG over policies, human-in-the-loop approval gates (for refunds/money), escalation/warm handoff, multi-turn memory, safety/guardrails, prompt-injection defense, cost controls/model routing, and evaluation (deflection, resolution, CSAT, incorrect-action rate).

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 13 glossary slice (LLM agent, ReAct, read/write split, action guard/approval gate, idempotency key, groundedness, containment/deflection, CSAT, prompt injection, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — when it's an agent vs. a bot, read/write split, grounding policies with RAG, approval gates, escalation, prompt injection, cost, and evaluation. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Intercom Fin, Klarna's assistant, Anthropic/OpenAI agent + tool-use guidance, RAG evaluation, and prompt-injection defense. |

> **How to use:** the graded core is **"LLM proposes, system verifies"** — read tools flow freely, write/money tools are validated and gated. Pair this with Chapter 7's agent fundamentals.
