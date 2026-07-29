# Common Interviewee Doubts — Chapter 1

Real questions candidates ask about the AI system design round before they walk in. Each answer ties back to a section of Chapter 1 so you can go deeper.

---

## A. "Which round am I even in?"

### Q1. Is the AI/ML system design round the same as the "general" system design round?
No — and confusing them is one of the most common preparation mistakes. Most large companies now run **two distinct design loops**:

- **General system design** — classic distributed systems: load balancers, sharded databases, caches, queues, consistency. (Design a URL shortener, a chat app.)
- **AI/ML system design** — ML-specific concerns: data pipelines, feature stores, training, offline/online inference, evaluation, drift, and increasingly LLM/RAG systems.

They overlap (you still reason about scale, latency, and fault tolerance in the AI loop) but are scored on **different rubrics by different interviewers against different bars**. This book is about the second one. *(See §"What an AI system design interview actually is".)*

### Q2. How do I find out which one I'm getting?
Ask your recruiter directly: "Is this a general system design round or an ML/AI system design round?" Recruiters will almost always tell you, and many companies (notably Meta) share prep materials that name the round. If you can't confirm, prepare for both and read the interviewer's opening prompt carefully — "design a recommendation system" signals ML design; "design a rate limiter" signals general design.

### Q3. Is this a coding round in disguise? How much code do I write?
It is not a coding round. You'll spend the hour drawing an architecture and talking through trade-offs, not writing production code. You may write a small snippet (a feature transformation, a data schema, a scoring formula) if it clarifies a point, but implementation speed is what the **coding round** measures, not this one. *(See §"What this round measures that coding rounds do not".)*

---

## B. How deep, how broad?

### Q4. How much ML theory do I actually need? Will they quiz me on math?
You need **fluency, not derivations.** You should be able to justify *why* a model type fits (e.g., "gradient-boosted trees for tabular features with limited data") and reason about evaluation metrics, but you will rarely be asked to derive backprop or write the softmax by hand. Applied Scientist loops lean more theoretical; ML Engineer and EM loops lean more operational. *(See §1.4 for how depth expectations shift by role.)*

### Q5. Should I go deep on the model, or spend time on data and infrastructure?
Both — and neglecting either is a classic failure mode. A strong answer treats **data, features, model, serving, evaluation, monitoring, and experimentation** as first-class. A common saying: a great ML system is "10% model, 90% everything else." Interviewers explicitly score ML-specific concerns *and* scalability/fault tolerance. *(See §1.2 "ML-Specific Concerns" and the scoring rubric.)*

### Q6. I've never worked at the scale they're describing (billions of users). Am I disqualified?
No. You're not expected to have operated it — you're expected to **reason about it**. Use back-of-the-envelope estimates, state assumptions ("assume 100M DAU, ~10 requests/user/day → ~12K QPS average, ~36K peak"), and design for those numbers. Showing structured estimation is itself a positive signal. *(Estimation gets a full treatment in Chapter 5.)*

### Q7. Do I need to memorize specific tools (Redis, Kafka, Feast, vLLM)?
Know a **representative example per category** and, more importantly, *why* you'd choose it. "A key-value store like Redis for sub-millisecond feature lookups" beats "Redis for speed." Naming a tool without a justification is weaker than describing the requirement and picking any reasonable option. *(See §1.2 "Trade-Off Articulation".)*

---

## C. Technology choices: agentic / LLM vs. traditional ML

### Q8. Should I default to an LLM or agentic design to look current?
**No.** Reaching for an LLM or a multi-agent system when a simpler model fits is a red flag — it signals you optimize for buzzwords over engineering judgment. Match the tool to the problem:

| If the problem is… | Prefer… |
|--------------------|---------|
| Tabular prediction, ranking, fraud, forecasting | Classical ML (GBTs, logistic regression) or deep ranking models |
| Retrieval/recommendation at scale | Embeddings + ANN retrieval + a ranking model |
| Open-ended language understanding/generation, Q&A over documents | LLM, often with RAG |
| A task needing planning, tool use, and multi-step autonomy | Agentic design — *and be ready to justify why a pipeline won't do* |

State the trade-offs explicitly: LLMs add latency, cost, non-determinism, and safety surface area. If you introduce one, say *why it's worth it*.

### Q9. When is an agentic architecture actually the right call in an interview?
Only when the task genuinely requires **autonomy + planning + tool use** (e.g., "design an assistant that books travel end-to-end"). For "classify this content" or "rank these items," an agent is over-engineering. A good move is to mention it as a *possible extension* ("we could layer an agent for the complex multi-step cases") rather than the default. *(Agentic systems are Chapter 7.)*

### Q10. The problem sounds like it could use GenAI. Do I have to bring it up?
Bring it up if it's relevant, but frame it as a deliberate choice with costs. If the interviewer wanted a classical solution and you force GenAI, you'll lose points; if GenAI genuinely fits and you ignore it, you'll seem out of date. Judgment — not defaulting either way — is what's scored.

---

## D. Time management (the 45–60 minute clock)

### Q11. How do I fit everything into 45–60 minutes?
Time-box it. A reliable split:

| Phase | Time | Goal |
|-------|------|------|
| Clarify & scope | 5–7 min | Requirements, scale, constraints, ML problem type |
| High-level design | 8–10 min | End-to-end architecture, data flow |
| Deep dive (ML + system) | 20–25 min | 1–2 components in depth |
| Trade-offs & extensions | 5–8 min | Failure modes, cost, future work |

Running out of time before discussing trade-offs is itself a red flag. *(Chapter 2 turns this into the full CHASE framework.)*

### Q12. I always over-spend on scoping. How much clarifying is too much?
Cap scoping at ~5–7 minutes, then commit. Asking a few sharp questions (scale, latency budget, must-have vs. nice-to-have) is a strong signal; interrogating for 15 minutes without drawing anything is not. State assumptions out loud and move: "I'll assume read-heavy, 50ms p99 budget — flag me if that's wrong."

### Q13. The interviewer keeps going deep on one component and now I'm out of time. Did I fail?
Not necessarily — interviewers often *drive* the deep dive intentionally. But manage it: "I can go deeper here, or zoom back out to cover monitoring and experimentation — which is more useful?" That hands them the steering wheel and shows time awareness.

---

## E. Communication & interacting with the interviewer

### Q14. Should I think out loud or design silently and present at the end?
Think out loud. This round is **collaborative** — the interviewer is a stakeholder, not a grader watching from behind glass. Silent design robs them of the reasoning they're there to evaluate. *(See §1.2 "The three high-level signals".)*

### Q15. The interviewer is giving me nothing — no nods, no hints. What do I do?
Neutral affect is normal and often deliberate. Keep signposting ("Now I'll design the serving layer…"), periodically check in ("Does this depth look right, or should I move on?"), and don't read silence as failure. Drive the conversation rather than waiting to be led.

### Q16. Is it okay to say "I don't know"?
Yes — paired with a plan. "I haven't used X in production, but here's how I'd reason about it / what I'd measure / how I'd de-risk it." Faking depth is far worse; interviewers probe, and bluffing collapses under follow-ups. Honesty plus a method reads as senior.

### Q17. Do I need to bring up responsible AI, privacy, or fairness unprompted?
For senior and staff+ roles, yes — a brief, relevant mention (privacy of user data, bias in training data, guardrails for generative outputs) signals maturity. Don't bolt on a generic "and we should be ethical" line; tie it to the actual design. Apple loops in particular weight privacy heavily. *(See §1.5.)*

---

## F. Role- and level-specific doubts

### Q18. I'm an Applied Scientist weak on infra (or a Data Engineer weak on modeling). How much does that hurt?
Interviewers calibrate by role. Applied Scientists get more latitude on infrastructure but must be rigorous on modeling, evaluation, and experiment design; Data Engineers can emphasize pipelines/feature serving but should still show how their data supports downstream ML. Know your role's expected weighting and cover the *other* areas at least at a "meets bar" level. *(See §1.4 role comparison table.)*

### Q19. What level am I being evaluated at, and can I influence it?
The same answer earns different ratings at different levels — the **bar shifts with seniority, not the rubric**. L4/L5: solid components and trade-offs. L6: cross-system, multi-team thinking. L7+: vision, strategy, ambiguity. You can push your perceived level up by proactively discussing scope, extensibility, and multi-year evolution — but only if the fundamentals are already solid. *(See §1.3.)*

### Q20. I'm interviewing as an EM. Do I need the same depth as an IC?
You need **enough** depth to lead ML teams credibly and to pressure-test a design, plus what ICs are not scored on: communication to non-technical stakeholders, resourcing/timeline awareness, and risk identification. You won't be expected to hand-optimize an inference kernel. *(See §1.4 "Engineering Manager".)*

---

## G. Company-specific doubts

### Q21. Do I really need to prepare differently for each company?
The fundamentals transfer, but emphasis differs enough to matter:

- **Google** — open-ended; expect scale and back-of-the-envelope math.
- **Meta** — structured ML rubric; go deep on data, features, evaluation, experimentation. (Meta also shares official prep materials — use them.)
- **Amazon** — leadership principles woven in; connect decisions to customer impact.
- **Microsoft** — product-grounded; consider enterprise constraints.
- **Apple** — privacy and on-device/edge.

*(See §1.5 and the company comparison matrix; the curated links live in `interview-prep-resources.md`.)*

### Q22. Should I mention a company's own systems (e.g., Spanner at Google, feature store at Meta)?
Lightly, and only if accurate. Referencing relevant internal-scale concepts shows homework, but don't name-drop for its own sake or pretend expertise you lack.

---

## H. Mindset & recovery

### Q23. I froze / went down a wrong path. Is the interview over?
No. Recovery is a scored skill. Name it ("Let me step back — that approach adds complexity without buying us much"), return to requirements, and pick a cleaner path. Gracefully correcting course often reads *better* than a flawless-but-lucky run.

### Q24. There are multiple valid designs — how do I know which one they want?
There usually isn't a single "right" answer; you're scored on the **quality of reasoning and trade-offs**, not on matching a hidden solution. Pick a defensible approach, state why, and acknowledge the main alternative and when you'd switch. *(See the coding-vs-design comparison in the chapter intro.)*

### Q25. How much does this one round matter?
A lot. For senior roles, the system design loop is often the single highest-leverage hour of the on-site — it's where committees decide your level and compensation. Strong performance can up-level you; weak performance can down-level you even when other signals are strong. It's the round most worth deliberate practice. *(See §"Why this round matters".)*

---

*Have a doubt that isn't covered here? Open an issue in the repo and it may be added.*
