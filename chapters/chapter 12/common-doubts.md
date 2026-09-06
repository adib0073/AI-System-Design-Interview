# Common Interviewee Doubts — Chapter 12 (Fraud & Anomaly Detection)

The questions candidates most often have about fraud/anomaly-detection rounds. Grouped by theme.

---

## Framing & metrics

**1. What's the core framing?**
**Cost-sensitive, real-time, adversarial detection under extreme imbalance.** Both errors cost money: a false negative is fraud losses; a false positive is a declined good customer (lost revenue + churn). You minimize **expected cost**, not error rate, and you do it in milliseconds on the money path against adapting attackers.

**2. Fraud is <1% of transactions — how do I handle imbalance?**
Don't optimize accuracy (predicting "all legit" is 99%+ accurate and useless). Use **PR-AUC**, cost-weighted loss, and resampling (careful undersampling / SMOTE with caveats). Report precision/recall at the chosen operating point, not accuracy.

**3. Which metric do I lead with?**
**PR-AUC** for model comparison under imbalance, plus a **cost matrix** to choose the threshold. Then business metrics: fraud $ caught, false-decline rate, and net dollar impact. ROC-AUC is misleading when positives are rare.

## Features & models

**4. What's the strongest signal?**
**Velocity features** — counts/amounts over recent windows (transactions per card/device/IP per minute/hour). Fraud is bursty. This requires **real-time aggregation** with low latency, which is a big part of the infra discussion.

**5. When do I use graph features?**
When fraud is organized. A **graph** over shared cards/devices/emails/addresses exposes **rings** that per-transaction models miss. Graph features or a GNN surface "this new account shares a device with 50 known-fraud accounts."

**6. Rules or ML — which?**
**Both, hybrid.** A **rules engine** gives speed, interpretability, hard compliance blocks, and instant response to a new attack (you can't retrain in an hour). ML catches subtle/novel patterns. Rules run alongside/ahead of ML. Saying "just use a neural net" misses how fraud teams actually operate.

**7. How do I catch novel fraud I've never seen?**
**Anomaly detection** (Isolation Forest, autoencoders) flags behavior unlike normal without needing fraud labels. Supervised models only catch fraud resembling past fraud; anomaly detection covers the new stuff. Use both.

## Decisions

**8. Is it just approve/decline?**
No — use a **tiered decision framework**. Low risk → allow; medium risk → **step-up authentication** (OTP/3DS/biometric); high risk → review or block. Step-up is the key idea: a legitimate user passes the challenge, a fraudster usually abandons — so you avoid declining good customers *and* avoid approving fraud.

## Labels & drift

**9. Why are labels hard?**
Two problems. (1) **Delayed:** chargebacks arrive weeks later, so recent data is unlabeled and noisy (not all chargebacks are fraud). (2) **Biased:** you only observe outcomes for transactions you **approved** — declined ones have no label. This is a selection-bias trap.

**10. What is reject inference and why care?**
Because you only see outcomes for approvals, your training data is biased toward "approvable" transactions. **Reject inference** estimates outcomes for rejected ones — or you keep a small **controlled hold-out** (approve some risky ones) to observe true outcomes. Mentioning this is a senior signal.

**11. How do I handle concept drift?**
Adversaries adapt, so fraud patterns shift constantly. Monitor performance and feature distributions, retrain frequently, use champion–challenger for safe rollout, and lean on anomaly detection for the newest attacks.

## Governance & delivery

**12. Anything special for money laundering / regulated fraud?**
**AML** requires **explainability and mandatory reporting** (SARs). You can't ship a black box; use interpretable models or explanations, and keep audit trails. Governance is a first-class requirement here.

**13. How do I structure the answer under time pressure?**
Clarify (fraud type, latency, cost of each error) → real-time features (velocity, graph) → hybrid rules + ML + anomaly detection → **tiered decision** (step-up) → labels (delayed/biased, reject inference) → drift/monitoring + champion–challenger → metrics (PR-AUC + cost). Keep cost-sensitivity and real-time front and center.
