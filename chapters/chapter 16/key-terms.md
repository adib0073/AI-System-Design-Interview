# Key Terms — Chapter 16 (Notifications & Delivery Optimization)

Interview-oriented definitions for the vocabulary in Chapter 16 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### The objective
- **Net value** — Predicted value (opens, downstream engagement, business) minus annoyance cost; the send/suppress criterion. *Why it matters:* **the core objective** — you send only when net value is positive, not whenever CTR is nonzero.
- **Annoyance / fatigue cost** — The modeled cost of an unwanted notification (mute/unsubscribe/uninstall risk, diminishing engagement) subtracted from value. *Why it matters:* the term that makes this different from ranking; a click isn't worth an uninstall.
- **Volume optimization** — Deciding how many notifications (including **zero**) to send each user to maximize long-term value under fatigue. *Why it matters:* the signature decision — often the best action is to send nothing.

### Volume & frequency control
- **Fatigue budget** — A per-user (often learned) limit on notification volume, allocated to the highest net-value candidates. *Why it matters:* turns "how many?" into a budget-allocation problem; spend it on the best candidates.
- **Frequency capping** — Hard limits on how many notifications a user receives per period/type. *Why it matters:* a simple, essential guardrail beneath the learned budget.
- **Global (send) budget / arbitration** — A shared per-user notification budget arbitrated across all teams/sources competing to notify. *Why it matters:* without central arbitration, every team spams the user independently; a platform-level necessity.

### Timing & channel
- **Send-time optimization (STO)** — Predicting the best time to deliver per user, within quiet hours and urgency. *Why it matters:* the right message at the wrong time is ignored (or annoying); a standard optimization lever.
- **Channel selection** — Choosing push / in-app / email / SMS per notification based on response, cost, urgency, and consent. *Why it matters:* channels differ in cost, intrusiveness, and consent rules; pick per message.
- **Consent / preference service** — The system enforcing opt-outs, per-channel preferences, and quiet hours as **hard constraints**. *Why it matters:* these are legal/UX hard limits, not optimizable — respect them absolutely.

### Measurement
- **Long-term holdout** — A group receiving no/minimal notifications to measure the system's true incremental effect on retention/engagement. *Why it matters:* short-term A/B rewards more sends; only a **long-term holdout** reveals whether notifications actually help or quietly drive users away.
- **Transactional vs. engagement/marketing** — Critical/expected notifications (order status, security) vs. optimizable, consent-gated promotional/engagement ones. *Why it matters:* transactional notifications bypass engagement suppression; conflating the two is a design error.

### Frontier
- **Interruption policy** — (Agentic) an agent's rule for whether reaching out to the user now is worth the interruption. *Why it matters:* the same net-value-under-fatigue decision, applied to proactive agents — the GenAI/agentic tie-in.

---

*Cross-refs:* ranking funnel, multi-objective value, uplift → Ch. 9/12. A/B and long-term metrics, guardrails → Ch. 8. GenAI content generation, agentic proactivity → Ch. 6/7/13. Churn/retention link → mock problem 01.
