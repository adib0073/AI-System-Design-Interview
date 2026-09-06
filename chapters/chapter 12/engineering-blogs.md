# Engineering Blogs & Papers — Chapter 12 (Fraud & Anomaly Detection)

Curated, interview-relevant reading. Focus on *system + cost* design (real-time features, tiered decisions, delayed labels), not just models. Search titles if links move.

## Start here (highest signal)
- **Stripe Radar** engineering posts — real-time ML fraud scoring, features, and the precision/recall business trade-off. Excellent end-to-end example.
- **PayPal / payments fraud** engineering write-ups — graph + sequence models on the money path.
- Overview of **cost-sensitive learning & PR-AUC** for imbalanced problems — why accuracy/ROC-AUC mislead.

## Real-time features & infra
- **Uber Michelangelo / real-time feature store** posts — low-latency features (velocity) for inference.
- **Feast / Tecton** feature-store material — online/offline parity for fraud features.
- Streaming aggregation write-ups (Kafka/Flink) — computing velocity features in real time.

## Graph-based fraud
- **Fraud ring detection with graphs / GNNs** — Amazon, Alibaba, and academic write-ups on entity-linking to expose rings.
- **Airbnb / Uber trust-and-safety** posts — graph and behavioral signals for account/marketplace fraud.

## Imbalance, anomaly & drift
- **Isolation Forest** (Liu et al., 2008) and **autoencoder anomaly detection** — unsupervised novel-fraud detection.
- **SMOTE** (Chawla et al., 2002) — resampling for imbalance (with caveats about synthetic minority points).
- **Concept drift** surveys — detection and adaptation for non-stationary streams.

## Account takeover & AML
- **Account-takeover detection** write-ups — behavioral biometrics, device fingerprinting, login velocity.
- **AML / transaction-monitoring** overviews — explainability and SAR-reporting constraints (governance-heavy).

## Labels & evaluation
- **Reject inference** literature (credit-scoring origins) — handling outcomes for declined cases.
- Delayed-feedback modeling (shared idea with Ch. 10 CVR) — training with labels that arrive late.

## How to use in prep
1. Read Stripe Radar's posts — they cover real-time features, imbalance, and the precision/recall/business trade-off concretely.
2. Be ready to justify **PR-AUC + cost matrix** over accuracy.
3. Have the **tiered decision + step-up auth** framing memorized.
4. Prepare a two-line answer on **delayed/biased labels and reject inference** for senior rounds.
