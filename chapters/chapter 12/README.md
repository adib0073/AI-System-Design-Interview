# Chapter 12 — Fraud & Anomaly Detection

Companion resources for Chapter 12. Fraud is defined by **extreme class imbalance**, **adversaries**, **delayed/biased labels**, and a **real-time money path** where both false negatives (fraud $) and false positives (declined good customers) are expensive.

Chapter 12 covers extreme imbalance, real-time features (velocity, graph), hybrid rules + ML, tiered decision frameworks (step-up auth), delayed/biased labels, reject inference, concept drift, anomaly detection for novel fraud, and money-path infrastructure/latency.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 12 glossary slice (velocity features, PR-AUC, cost matrix, step-up auth, reject inference, concept drift, graph/GNN, chargeback, ATO, AML, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — imbalance, why PR-AUC, rules + ML, tiered actions vs. binary decline, delayed labels/reject inference, and drift. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Stripe/PayPal/Airbnb/Uber fraud engineering, graph-based fraud, imbalanced learning, and real-time feature systems. |

> **How to use:** anchor on **cost-sensitive, real-time, adversarial** — and the **step-up authentication** idea (add friction instead of hard-declining). That framing separates a fraud answer from a generic classifier.
