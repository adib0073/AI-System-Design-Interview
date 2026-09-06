# Common Interviewee Doubts — Chapter 18 (Deep Research & Planning Agent)

The questions candidates most often have about deep-research/planning-agent rounds. Grouped by theme.

---

## Framing

**1. What's the framing that impresses immediately?**
It's a **long-horizon, multi-agent, transactional** problem, and you must **separate planning (safe, reversible) from execution (money, irreversible)**. An orchestrator decomposes the goal, sub-agents research in parallel, you synthesize a grounded/cited plan, replan as constraints change, and only then book — behind human approval, with idempotent transactions and rollback.

**2. Isn't this just one big ReAct loop?**
No — that under-designs it. It needs **orchestration, parallelism, and durable state**. And "book the flight" isn't just another tool call — it's a money-moving write with partial-failure and rollback semantics. Modeling it as a single loop is the common trap.

## Multi-agent

**3. Why orchestrator + sub-agents instead of one agent?**
Because the research is **parallelizable and separable** (flights, hotels, activities). Fan-out gives speed, specialization, and larger effective context. But it **multiplies cost and coordination complexity** — so use it deliberately.

**4. When would you NOT use sub-agents?**
For linear/sequential or cheap tasks where one grounded agent suffices. Fan-out multiplies token cost and adds coordination/merge complexity. Naming this cost (per Chapter 7's simplicity principle) is a maturity signal.

## Grounding & synthesis

**5. How do I keep the plan trustworthy?**
Sub-agents call **live tools** (never guess prices/availability), every bookable fact is **cited**, synthesis is **verified feasible** against constraints, and prices are **re-confirmed live before charging**. Faithfulness + citations, not model memory.

**6. The price found during research is stale by the time the user approves — what do you do?**
Treat research prices as estimates and **re-verify live before charging**. If it moved beyond tolerance, replan or re-confirm with the user. Handling staleness is a real-systems signal.

## Transactions (the crux)

**7. The flight books but the hotel is now sold out — what happens?**
This is *the* question. Use **saga / compensation**: cancel/refund the booked flight or hold and replan the hotel, communicate honestly, and never leave a half-booked trip with a charge. Combine with **idempotency keys** so retries don't double-book.

**8. Can you make the whole booking atomic?**
Not truly — you can't do a 2-phase commit across independent airlines/hotels. Don't claim ACID; design **compensating actions**, idempotent retries, and clear failure communication instead.

## Human control & autonomy

**9. How much can it do on its own?**
Research and planning fully autonomously (reversible). **Spending requires explicit, scoped consent** with hard caps. Principle: reversible actions can be autonomous; irreversible/money actions need a human gate. State this crisply.

**10. Prompt injection from a web source tells the agent to book something — is that a risk?**
Yes — treat retrieved/web content as **untrusted data**, constrain actions, and rely on the **human approval gate** on spend so injected instructions can't move money on their own.

## Durability & cost

**11. It's an 8-minute task and the server restarts at minute 6 — do you lose it?**
No, with **durable orchestration + checkpointing** it resumes from the last step, and idempotency prevents re-booking. An in-memory loop loses the task or double-books.

**12. Multi-agent fan-out just 10x'd your token bill — how do you control it?**
Bound sub-agent count/depth with per-agent budgets, **route models** (small for simple, large for planning/synthesis), cache tool results, stop early, and track **cost-per-task**.

## Evaluation & delivery

**13. How do you evaluate an open-ended plan with no single right answer?**
Rubric scoring (feasibility, budget, preference match, faithfulness) via human/LLM-judge, plus **component evals** (retrieval, synthesis, replanning) and **trace inspection**, and online acceptance/booking-success/cost-per-task. Don't evaluate only the final plan — a good answer via a broken/expensive process won't generalize.

**14. How do I structure the answer under time pressure?**
Clarify (research-only vs. + booking, constraints, autonomy) → orchestrator + parallel sub-agents → grounded/cited synthesis → **plan → check → replan** → **transactional booking** (idempotency, saga/compensation, re-verify price) → **approval gate** + bounded autonomy → memory/**durable orchestration** → cost/latency (fan-out caps, routing) → evaluation. Keep plan-vs-execute separation and durable/transactional design central.
