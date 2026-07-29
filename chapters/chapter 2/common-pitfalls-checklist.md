# Common Pitfalls Checklist

Run through this the night before an interview, and use it to grade your mocks. Each item is a mistake candidates actually make in AI system design rounds — with the fix. (Drawn from the pitfalls flagged throughout Chapter 2.)

---

## Phase C — Clarify & Scope
- [ ] **Jumping straight to design.** → Spend 5–7 min scoping first; most failures happen in the first 10–15 minutes.
- [ ] **Rushing clarification and solving the wrong problem.** → Probe product context, scale, constraints, success metrics before drawing.
- [ ] **Not writing anything down.** → Keep a short requirements doc on the board to anchor later decisions.
- [ ] **Not stating assumptions.** → Say them out loud ("Assume 100M DAU, p99 < 100 ms"); the interviewer will correct if wrong.
- [ ] **Over-interrogating.** → Cap scoping and commit; 15 minutes of questions with no diagram is also a failure.

## Phase H — High-Level Design
- [ ] **Spending >10 minutes perfecting the diagram.** → It's a trap; it starves the deep-dive phases.
- [ ] **Messy, unlabeled diagram.** → Label components *and* arrows ("User request", "Features", "Predictions", "Events"); erase and redraw if cluttered.
- [ ] **Mixing offline and online into one tangle.** → Separate them with color/line style or two diagrams.
- [ ] **Treating the first draft as final.** → Say it's a first pass; leave margin to refine after Phases A and S.

## Phase A — AI/ML Deep Dive
- [ ] **Superficial model treatment.** → A massive red flag (especially at Meta); justify the choice via trade-offs.
- [ ] **Ignoring data & labeling.** → Cover sources, collection (stream vs. batch), and implicit/explicit label generation.
- [ ] **Skipping the feature store / train-serve skew.** → Explain how training and serving features stay consistent.
- [ ] **Metrics with no business link.** → Connect offline → online (A/B) → business metrics.
- [ ] **No experimentation / versioning story.** → Mention experiment tracking, data/feature/model versioning, triggers.

## Phase S — System & Infra Deep Dive
- [ ] **Over-focusing on ML and ignoring infra (or vice versa).** → Phases A and S each deserve substantial time.
- [ ] **"Just use autoscaling" with no signal.** → Justify the trigger (QPS, queue depth, GPU utilization, p99); note HPA vs. KEDA, node autoscalers, container cold start.
- [ ] **No named bottleneck.** → Call out feature-store throughput, GPU memory, or network latency.
- [ ] **Forgetting caching pitfalls.** → Discuss invalidation (stale predictions), cache stampede, eviction (LRU), global vs. local.
- [ ] **No observability.** → Cover model performance, data drift, p50/p95/p99, business impact, and alerts.
- [ ] **Infra choices untethered to requirements.** → Every infra decision ties back to an ML or product requirement.

## Phase E — Extensions & Trade-offs
- [ ] **Running out of time before trade-offs.** → Protect this phase; reaching it is itself a positive signal.
- [ ] **No edge cases / failure modes.** → Cold start, stale features, drift, model failure.
- [ ] **No cost or future-improvement discussion.** → Mention cost optimization and a responsible-AI guardrail.

## Communication pitfalls (evaluated as much as content)
- [ ] **Silent design.** → Narrate while drawing; unheard reasoning can't be scored.
- [ ] **Being passive / waiting to be led.** → Propose the next step; it signals ownership and time awareness.
- [ ] **Ignoring the interviewer's cues.** → If they want depth somewhere, switch immediately.
- [ ] **Never pausing for feedback.** → Check in after each major step ("Does this align with what you had in mind?").
- [ ] **Rambling / no structure.** → Use signposting to guide them through your thinking.
- [ ] **Getting defensive about suggestions.** → Acknowledge and incorporate good points.
- [ ] **Getting stuck and freezing.** → Pause, break it down, ask for a nudge, or propose-and-iterate.

## Company-fit pitfalls
- [ ] **Google:** not asking about scale early / no back-of-the-envelope math / not leading with trade-offs.
- [ ] **Meta:** skipping a rubric step (Data → Features → Model → Training → Serving → Eval → Experimentation) or treating A/B testing as an afterthought.
- [ ] **Amazon:** not tying decisions to customer impact; not showing end-to-end ownership; over-engineering instead of shipping pragmatically.

---

> **One-line reminder:** *Structure beats brilliance.* Cover all five phases, balance ML and infra, name your trade-offs, and keep talking.
