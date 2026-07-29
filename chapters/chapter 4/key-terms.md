# Key Terms — Chapter 4 (Core AI System Concepts)

Interview-oriented definitions for the AI-lifecycle vocabulary in Chapter 4. Each entry pairs a crisp definition with *why it matters* in a design round. Terms defined in earlier chapters are cross-referenced. Feeds the cumulative book glossary.

---

### Problem framing & tasks
- **AI vs ML** — AI is the broad field of intelligent behavior; ML is the subset that learns patterns from data. *Why it matters:* used interchangeably in practice; name the specific technique (classical ML, DL, GenAI, agentic) when precision matters.
- **Learning paradigms** — Supervised (labeled), unsupervised (unlabeled patterns), reinforcement (reward feedback), self-supervised (labels created from the data). *Why it matters:* self-supervised underpins foundation models; state which paradigm your problem is.
- **Task formulation** — Classification, regression, ranking, retrieval, generation, clustering, anomaly detection. *Why it matters:* the formulation dictates the model family *and* the offline metric.
- **Multi-stage funnel** — Candidate generation → ranking → re-ranking. *Why it matters:* the standard pattern for search/recs/ads; keep early stages cheap, spend compute on the small final set.

### Metrics & evaluation
- **Three-tier evaluation** — Offline → online → business metrics, explicitly chained. *Why it matters:* optimizing offline AUC alone is the #1 red flag; connect a model gain to user and business impact.
- **Offline metrics** — Precision/Recall, F1, AUC-ROC, PR-AUC (classification); Recall@k, Precision@k, MRR, NDCG (retrieval/ranking). *Why it matters:* match the metric to the task and class balance (PR-AUC for imbalance).
- **Online metrics** — CTR, conversion, dwell time, latency — measured on live users. *Why it matters:* the real signal; a perfect-but-slow model is useless.
- **Business metrics** — ARR, churn, CSAT/NPS, GMV. *Why it matters:* what executives care about; senior candidates tie technical wins to these.
- **A/B testing** — Randomized control vs treatment to measure causal impact. *Why it matters:* the gate for shipping; needs statistical significance and guardrail metrics.
- **Interleaving** — Mixing two rankers' results in one list to compare sensitively. *Why it matters:* faster/cheaper than A/B for ranking changes.
- **Multi-armed bandit (MAB)** — Dynamically shifts traffic toward better-performing options. *Why it matters:* reduces the opportunity cost of exploring vs a fixed A/B split.
- **Golden set** — Small, hand-labeled (or synthetically generated) set for regression testing. *Why it matters:* catches quality regressions on critical cases; essential for GenAI.
- **Hold-out set** — Data unseen during training for unbiased generalization estimates. *Why it matters:* baseline offline evaluation.
- **Backtesting** — Replaying historical logs to score a candidate model retrospectively. *Why it matters:* cheap pre-release validation against known outcomes.
- **Human evaluation** — Raters score outputs for fluency/safety/helpfulness. *Why it matters:* the gold standard for generative/LLM quality where automatic metrics fall short.
- **Evaluation beyond accuracy** — Fairness, robustness, calibration, latency, cost. *Why it matters:* high average accuracy can hide systematic or ethical failures.

### Data engineering
- **Data quality dimensions** — Completeness, consistency, accuracy, freshness. *Why it matters:* set thresholds + automated monitoring; data usually beats model choice.
- **Data labeling approaches** — Manual, programmatic/weak supervision, active learning, semi-/self-supervised. *Why it matters:* active learning + weak supervision cut labeling cost at enterprise scale.
- **Active learning** — Model picks the most informative samples to label next. *Why it matters:* maximizes label ROI when annotation is expensive.
- **Weak supervision** — Generating noisy labels from heuristics/rules (e.g., Snorkel). *Why it matters:* bootstraps labels when hand-labeling doesn't scale.
- **Data versioning (DVC / LakeFS)** — Git-like versioning for datasets / data lakes. *Why it matters:* reproducibility and rollback; "data evolves like code."
- **Batch vs streaming pipelines** — Scheduled high-throughput vs near-real-time ingestion. *Why it matters:* batch for training data/analytics; streaming for online features and live dashboards.
- **Differential privacy (DP)** — Calibrated noise so no single record materially changes output. *Why it matters:* signals "privacy by design" under GDPR/HIPAA.
- **Federated learning (FL)** — Training across devices; only model updates leave the device. *Why it matters:* keeps raw sensitive data local; shows distributed-systems + privacy maturity.

### Features
- **Feature store** — Central source of truth for features across training and serving (online + offline stores). *Why it matters:* prevents training-serving skew, enables reuse and low-latency retrieval.
- **Online vs offline features** — Precomputed/stored vs computed at inference time. *Why it matters:* precompute stable/expensive features, compute volatile ones live, then merge.
- **Training-serving skew (feature drift)** — Features differ between training and serving due to different logic/timing/sources. *Why it matters:* a top cause of "great offline, bad online"; the feature store is the fix.
- **Point-in-time correctness** — Joining features as of the label's timestamp. *Why it matters:* prevents data leakage from the future — a subtle but fatal bug.
- **Feature selection** — Filter (correlation/MI), wrapper (RFE), embedded (L1/Lasso, tree importance); SHAP/attention for interpretability. *Why it matters:* fewer, better features reduce cost and improve generalization.

### Models
- **Classical ML** — Linear/logistic, trees, SVM, kNN on structured data. *Why it matters:* often the right, cheap default for tabular problems.
- **Ensemble methods** — Bagging, boosting (GBT/XGBoost/LightGBM), stacking. *Why it matters:* GBTs are frequently the strongest tabular baseline.
- **Deep learning** — Multi-layer nets (CNN, RNN/LSTM, Transformer) for unstructured data. *Why it matters:* the choice for images/audio/text/sequences.
- **Foundation model** — Large pretrained model (BERT/GPT/CLIP/Llama) adapted via prompt/fine-tune. *Why it matters:* fewer labels, fast to build; but compute cost and nondeterminism.
- **Hosted vs open-weight LLM** — API model (GPT/Claude/Gemini) vs self-hostable (Llama/Qwen/Gemma). *Why it matters:* different cost, latency, privacy, and customization profiles.
- **Embedding model** — Encodes text/image/audio into dense vectors. *Why it matters:* the producer side of every vector DB and retrieval system.
- **Bi-encoder vs cross-encoder** — Fast independent embeddings (retrieval) vs slow joint scoring (re-ranking). *Why it matters:* the two-stage retrieve-then-rerank pattern; a cross-encoder on top-k is a quality step-change.
- **Re-ranking model** — Second-stage model that reorders retrieved candidates. *Why it matters:* small latency cost for large recall@k/precision@k gains in search/RAG.

### GenAI approaches
- **Prompting (zero/few-shot)** — Steering a model via instructions/examples, no training. *Why it matters:* cheapest, fastest first option.
- **RAG (retrieval-augmented generation)** — Retrieve (→ re-rank) → generate grounded answers. *Why it matters:* injects fresh/private facts without retraining; reduces hallucination and enables citations.
- **Fine-tuning (LoRA/QLoRA)** — Adapting a base model to a domain/style; LoRA trains a small parameter set. *Why it matters:* for behavior/style/skill, not lookup facts; LoRA cuts memory/cost.
- **Agentic AI** — LLM plans, calls tools/APIs, observes, and iterates. *Why it matters:* multi-step tasks; fans out to 5–20× more LLM calls — size capacity on LLM QPS.
- **Prompt registry** — Versioned store for prompts/templates alongside the model registry. *Why it matters:* rollback + lineage for prompts, which behave like deployable artifacts.

### Training infra
- **Data / model / pipeline parallelism** — Split the batch across GPUs (full model copy each) / split the model across GPUs / split layers into staged micro-batches. *Why it matters:* data parallelism for throughput; model/pipeline when the model exceeds one GPU.

### Serving, MLOps & lifecycle
- **Serving modes** — Batch, nearline, real-time. *Why it matters:* match the mode to the latency requirement.
- **Model optimization** — Quantization, pruning, distillation. *Why it matters:* fit heavy models on limited/edge hardware; cut latency and cost.
- **MLOps** — DevOps for ML: CI/CD, monitoring, governance, automated retraining. *Why it matters:* turns a prototype into a reliable production system.
- **Model registry** — Stores artifacts, metadata, versions; supports promotion/rollback/lineage (MLflow, SageMaker, Vertex). *Why it matters:* safe releases and auditability.
- **Data drift / concept drift / prediction drift** — Input `P(X)` shifts / relationship `P(Y|X)` shifts / output distribution shifts (early warning). *Why it matters:* the three signals monitoring must track to trigger retraining.
- **Retraining triggers** — Scheduled, performance-drop, drift-threshold, or enough new labels. *Why it matters:* automate trigger → deploy with a rollback path.
- **Shadow deployment** — Run the new model in parallel, log only, no user impact. *Why it matters:* validates parity/stability before exposure.
- **Canary deployment** — Route a small traffic slice to the new model first. *Why it matters:* limits blast radius; pair with A/B and rollback.
- **Implicit vs explicit feedback** — Clicks/dwell/purchases (abundant, noisy) vs ratings/reports (sparse, clearer). *Why it matters:* systems lean on implicit volume; explicit for evaluation/high-value signals.
- **Continuous learning** — Online/incremental training on evolving streams, with logging/replay and human-in-the-loop. *Why it matters:* adaptivity vs stability trade-off; needs strong monitoring.

---

*Cross-refs:* QPS/latency/CAP/caching/observability → Chapter 3 key-terms. Interview framing (offline→online→business, "does this need ML") → Chapter 1/2. GPU/KV-cache/training-cost sizing → Chapter 5.
