# Common Interviewee Doubts — Chapter 16 (Notifications & Delivery Optimization)

The questions candidates most often have about notification-system rounds. Grouped by theme.

---

## The objective (get this right first)

**1. What should the system optimize?**
**Long-term value minus annoyance/fatigue — not short-term clicks.** A notification that earns one click but pushes the user to mute or uninstall is a net loss. The send/suppress decision is: is **net value** (engagement + downstream + business value − annoyance cost) positive? Lead with this.

**2. Why is optimizing CTR/opens a trap?**
Because you can always send more to get more clicks in the short term — while quietly increasing churn. Click-maximizing systems over-notify. The correct objective explicitly subtracts fatigue and is validated over the **long term**.

## Volume optimization (the signature idea)

**3. What's the key decision that makes this different from ranking?**
**Volume optimization** — deciding *how many* notifications to send each user, including **zero**. Ranking assumes you're showing something; here the best action is often to stay silent. Frame "how many?" as allocating a **fatigue budget** to the highest net-value candidates.

**4. What's a fatigue budget?**
A per-user (often learned) cap on notification volume based on their sensitivity. You then spend that budget on the highest net-value candidates and suppress the rest. Simple **frequency caps** sit underneath as hard guardrails.

**5. Multiple teams all want to notify the same user — what do I do?**
A **global send budget with arbitration**: a shared per-user budget that all sources compete for, arbitrated centrally by net value. Without it, every team spams independently and the user drowns. This platform-level point impresses.

## Timing, channel & consent

**6. How do I pick send time and channel?**
**Send-time optimization** predicts the best delivery time per user (respecting quiet hours/urgency). **Channel selection** picks push/in-app/email/SMS by response, cost, intrusiveness, and consent. Both are optimization layers on top of the send/suppress decision.

**7. How do consent and quiet hours fit?**
As **hard constraints**, not optimization targets. Opt-outs, per-channel preferences, and quiet hours are enforced absolutely by a consent/preference service — legal and UX non-negotiables.

**8. Are all notifications optimizable?**
No. **Transactional** notifications (order status, security alerts, 2FA) are expected and bypass engagement suppression. Only **engagement/marketing** notifications are consent-gated and volume-optimized. Conflating them is a design error.

## Measurement (the hard part)

**9. How do I measure whether notifications actually help?**
A **long-term holdout** — a group that receives no/minimal notifications — measured over weeks/months on retention/engagement. Short-term A/B rewards sending more; only the long-term holdout reveals the true incremental effect (and whether you're driving users away). This is the most important measurement point.

**10. Should I use uplift modeling?**
Yes — target notifications at users whom they'll actually move (persuadables), not those who'd engage anyway or would be annoyed. Same idea as churn/marketing uplift (mock problem 01).

## GenAI / agentic angles

**11. Where does GenAI fit?**
As a **content lever**: generate/personalize notification copy (subject lines, body) to lift relevance — measured within the same net-value framework and guardrails. It improves the *content*, not the send/suppress *decision*.

**12. What's the agentic angle?**
An **interruption policy**: when a proactive agent decides whether to reach out now, it's the same net-value-under-fatigue decision. Framing notifications as "agent interruption decisions" ties this chapter to the agentic ones (13/17/18).

## Delivery

**13. How do I structure the answer under time pressure?**
Clarify (notification types, channels, goal) → **objective (net value = value − annoyance)** → relevance ranking + **volume optimization (fatigue budget, incl. zero)** → send-time + channel + consent constraints → **global budget arbitration** → transactional vs. engagement split → measurement (**long-term holdout**, uplift) → GenAI content + agentic interruption. Keep "long-term value minus fatigue" and "sending zero is valid" central.
