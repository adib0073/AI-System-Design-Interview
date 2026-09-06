# Engineering Blogs & Papers — Chapter 13 (Agentic Customer Support)

Curated, interview-relevant reading. Focus on *safe action-taking* (read/write split, gates, evaluation), not just chat quality. Search titles if links move.

> **Living note:** the agent-framework and eval ecosystem moves fast — treat tooling entries as directional.

## Start here (highest signal)
- **ReAct: "Synergizing Reasoning and Acting in Language Models"** (Yao et al., 2022) — the core agent loop. Read first (also referenced in Ch. 7).
- **Anthropic "Building effective agents"** — when to use agents vs. workflows, tool design, and keeping it simple. Excellent design guidance.
- **OpenAI function calling / tools guides** — structured tool invocation patterns.

## Real-world support agents
- **Intercom "Fin"** engineering/product write-ups — RAG-grounded support answers, resolution-rate framing, and guardrails.
- **Klarna AI assistant** reports — scale of deflection and the human-handoff trade-offs (read critically; vendor claims).
- **Sierra / Decagon / Ada** (support-agent vendors) — public material on action-taking agents and evaluation.

## Grounding & RAG evaluation
- **RAGAS** and faithfulness/groundedness metrics — measuring whether answers are supported by retrieved policy.
- RAG design posts (chunking, hybrid retrieval, reranking) — see Chapter 6 index for depth.

## Safety & prompt injection
- **OWASP Top 10 for LLM Applications** — prompt injection, insecure output handling, excessive agency. Directly maps to the read/write split and action guards.
- **Simon Willison's prompt-injection writing** — why prompt-level defenses are insufficient and system-level controls are needed.

## Evaluation & observability
- **LLM-as-a-judge** references — scoring groundedness and helpfulness at scale.
- Agent-observability/tracing tools (LangSmith, etc.) — capturing trajectories for debugging non-deterministic agents.

## How to use in prep
1. Read ReAct and Anthropic's "Building effective agents" — they anchor the loop and the "keep it simple / gate the risky actions" philosophy.
2. Memorize the **read/write split + action guard + idempotency** pattern.
3. Have the **deflection + resolution + CSAT + incorrect-action-rate** metric set ready.
4. Prepare a crisp **prompt-injection** answer emphasizing system-level (not prompt-level) defense.
