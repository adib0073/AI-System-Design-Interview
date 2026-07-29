# Common Interviewee Doubts — Chapter 2

Questions candidates ask about the CHASE framework, time management, and adapting to company styles. Each answer ties back to Chapter 2.

---

## A. About the framework itself

### Q1. Is CHASE the "official" framework? What if my interviewer has their own structure?
CHASE (Clarify & Scope → High-Level Design → AI/ML Deep Dive → System & Infra Deep Dive → Extensions & Trade-offs) is a **default template, not a straitjacket.** Its job is to guarantee you cover every evaluation area under time pressure. If the interviewer steers you elsewhere, follow them — the phases still work as a mental checklist of what not to forget. *(See §"CHASE: A five-phase interview framework".)*

### Q2. Do I have to go through the phases strictly in order?
The order is deliberate (you can't design before scoping), but it's iterative. The chapter is explicit that your first high-level diagram isn't final — you refine it after the deep dives. Announce that ("this is a first pass; I'll refine it after we go deeper").

### Q3. How strictly should I follow the time boxes?
Treat them as guardrails, not a stopwatch. The key failure modes they prevent are: rushing Phase C, over-perfecting the Phase H diagram (>10 min is a trap), and running out of time before Extensions. If you're past a phase's upper bound and the interviewer hasn't pulled you there, move on and say so.

---

## B. Time management

### Q4. The interview is 45 minutes — do I really only get ~35 for design?
Yes. Plan for the first 5–10 minutes to go to introductions and understanding the problem. A 45-min round leaves ~35–40 min of design time; a 60-min round leaves ~50. That's exactly why a time-boxed structure matters. *(See §"CHASE".)*

### Q5. What if I run out of time before Phase 4 (Infra) or Phase 5 (Extensions)?
Two defenses: (1) don't overspend early — Phase C ≤ 7 min, Phase H ≤ 10 min; (2) if you're behind, compress by breadth — quickly name what you'd cover ("I'd also add drift monitoring and a prediction cache") rather than skipping silently. Reaching trade-offs at all is a positive signal, so protect it.

### Q6. I always over-spend on the high-level diagram. How do I stop?
Set a hard 10-minute ceiling for Phase H and treat "perfecting the diagram" as a known trap. Draw it clean-enough, label the arrows, say it's a draft, and move into the deep dives where most of the score lives.

---

## C. Depth, breadth, and your role

### Q7. Phase 3 (ML) vs Phase 4 (Infra) — where should I spend more time?
Both deserve substantial time; over-indexing on one is a classic mistake. Then use the **T-shape**: cover everything for breadth, and go deep in the 1–2 areas matching your background (an ML engineer → training/feature store; an infra engineer → serving/scaling). Signal it: "I've done most of my recent work on the training pipeline — happy to go deep there." *(See §"The T-shaped answer".)*

### Q8. How do I show senior/staff-level thinking specifically?
Staff signals concentrate in Phase 5 and in how you handle ambiguity: edge cases and failure modes, cost optimization, multi-year improvements, and framing an underspecified problem. The chapter also calls out staff-level infra topics — container **cold start**, warm pools, data retention policies, cache trade-offs (hit rate vs. accuracy, memory/eviction, global vs. local).

### Q9. Should I drive the whole conversation or wait for the interviewer?
Drive it — passivity reads as a lack of initiative. Propose the next step ("I've covered training; let's do serving next"), but follow their cues instantly when they want depth or a change of direction. *(See §"Driving the conversation vs. being passive".)*

---

## D. Requirements, assumptions, and diagrams

### Q10. When should I state an assumption vs. ask the interviewer?
Ask when the answer materially changes the design and is cheap to get (scale, latency budget). When the interviewer deflects ("what do you think?"), state a reasonable assumption explicitly and proceed — that's the expected behavior, especially for staff/principal candidates who should fix the scope themselves.

### Q11. Should I draw one diagram or separate offline and online?
Separate the offline (training/data) path from the online (serving) path using different colors or line styles — or two diagrams if one gets messy. Label every arrow. Clarity beats completeness. *(See §"Whiteboarding high-level designs".)*

### Q12. How much should I write in the "requirements doc"?
Just enough to anchor decisions: the key functional requirements, the non-functional numbers (latency, QPS, availability), and your stated assumptions. It signals organization and gives you something to point back to later.

---

## E. Company adaptation

### Q13. How do I know which company style I'm facing, and how much does it change?
Confirm the format with your recruiter. The CHASE phases stay the same; the **emphasis** shifts:
- **Google** — scale + trade-offs; expect open-ended prompts and 10× stress tests.
- **Meta** — march the ML rubric (Data → Features → Model → Training → Serving → Eval → Experimentation); A/B testing built in, not bolted on.
- **Amazon** — Leadership Principles woven into design choices; tie everything to customer impact.
*(See §"Company-specific guidelines".)*

### Q14. Amazon combines design with behavioral — how do I handle Leadership Principles in a design round?
Weave them into decisions naturally: Customer Obsession (tie choices to user benefit), Dive Deep (justify with detail), Ownership (mention monitoring/rollback), Frugality (cost-aware trade-offs). Have 2–3 LP stories ready in case they ask "tell me about a time when…" mid-design.

### Q15. Should I name company-specific tech (two-tower models, integrity signals for Meta)?
Lightly and only if accurate — it shows homework. For Meta, large-scale recommendation, two-tower models, engagement optimization, and integrity signals are relevant touchpoints. Don't force them where they don't fit.

---

## F. Communication & mindset

### Q16. Thinking out loud feels unnatural. How do I get better?
It's a trained habit. In every mock, narrate while you draw ("here the event stream feeds the feature store…") and practice the signposting phrases (see `signposting-and-recovery-scripts.md`). The interviewer cannot score reasoning they can't hear.

### Q17. What do I do the moment I get stuck?
Use the recovery ladder: pause and acknowledge → break the problem into sub-parts → ask for a nudge → propose-and-iterate. Interviewers are usually supportive when they see a structured approach. *(See §"How to recover when stuck".)*

### Q18. I realized my high-level design was wrong halfway through. Is it over?
No — course-correcting gracefully is a positive signal. Step back, say what doesn't hold and why, and take the cleaner path. This is expected, since the first diagram is explicitly a draft.

---

*Missing a doubt? Open an issue in the repo and it may be added.*
