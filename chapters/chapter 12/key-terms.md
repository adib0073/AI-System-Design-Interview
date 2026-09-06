# Key Terms — Chapter 12 (Fraud & Anomaly Detection)

Interview-oriented definitions for the vocabulary in Chapter 12 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Imbalance & metrics
- **Extreme class imbalance** — Fraud is a tiny fraction (often <1%) of transactions. *Why it matters:* accuracy is useless; shapes sampling, loss weighting, and metric choice.
- **PR-AUC** — Area under the precision-recall curve. *Why it matters:* the right summary metric under extreme imbalance (ROC-AUC and accuracy are misleading when positives are rare).
- **Cost matrix** — Weighting of false negatives (fraud $) vs. false positives (false-decline cost). *Why it matters:* fraud is **cost-sensitive**; pick the operating point that minimizes expected cost, not error rate.

### Features & models
- **Velocity features** — Counts/sums over recent time windows (e.g., transactions per card per hour). *Why it matters:* the single strongest fraud signal; requires low-latency real-time aggregation.
- **Graph features / GNN** — Features (or graph neural nets) over entities linked by shared card/device/address/email. *Why it matters:* expose fraud **rings** that per-transaction models miss.
- **Anomaly detection** — Unsupervised methods (Isolation Forest, autoencoders) flagging behavior unlike normal. *Why it matters:* catches **novel/unlabeled** fraud that supervised models trained on past fraud can't.
- **Behavioral biometrics** — Signals like typing/mouse/session patterns. *Why it matters:* verify a user is who they claim; strong against account takeover.
- **Rules engine** — Fast, interpretable, deterministic checks (blocklists, velocity limits, compliance). *Why it matters:* run alongside/ahead of ML for speed, hard compliance, and instant response to new attacks.

### Decisions & actions
- **Step-up authentication** — Adding friction (3DS/OTP/biometric/KYC) for medium-risk cases instead of hard-declining. *Why it matters:* the key insight — a legitimate user passes, a fraudster usually fails; avoids the binary approve/decline trap.
- **Tiered decision framework** — Actions scaled by risk: allow → step-up → review → block. *Why it matters:* lets you act under uncertainty and preserve good customers.

### Labels & their problems
- **Chargeback** — A card-network reversal (often weeks later) serving as a delayed fraud label. *Why it matters:* labels arrive **late** and are noisy (not all chargebacks are fraud); complicates training/eval.
- **Reject inference** — Estimating outcomes for declined transactions (which have no natural label), or a controlled hold-out that lets some through to observe outcomes. *Why it matters:* you only see outcomes for what you *approved*, biasing training — the fraud analog of selection bias.
- **Concept drift** — Change in the data/fraud distribution over time, largely driven by adversaries adapting. *Why it matters:* models decay fast; requires monitoring and frequent retraining.

### Related fraud types
- **Account takeover (ATO)** — An attacker gaining control of a legitimate account. *Why it matters:* detected via behavioral/device deviation and login velocity — different signals than payment fraud.
- **AML (Anti-Money-Laundering)** — Regulated detection of money laundering (e.g., structuring). *Why it matters:* **explainability and reporting (SARs) are mandatory** — a governance constraint, not just accuracy.
- **Champion–challenger** — Running a new model in shadow against the incumbent and promoting on cost metrics. *Why it matters:* safe deployment on the money path where mistakes are expensive.

---

*Cross-refs:* real-time feature stores, streaming, latency → Ch. 3/4. Imbalance/metrics → Ch. 4. Adversarial/coordination & graph signals → Ch. 11. Drift, monitoring, governance/explainability → Ch. 8.
