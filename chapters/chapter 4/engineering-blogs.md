# Engineering-Blog Index — AI/ML Platforms, Feature Stores & Evaluation

Curated reading on the Chapter 4 lifecycle: **ML platforms, feature stores, data/labeling, evaluation & experimentation, serving, and MLOps/monitoring**. These are the write-ups interviewers recognize when you cite them.

> **Link maintenance:** blog URLs move. If a deep link 404s, search the title on the linked root. Last reviewed: 2026.

---

## End-to-end ML platforms
- **Uber — Michelangelo: Uber's Machine Learning Platform** — the canonical "platform" reference; introduced the feature-store idea to a wide audience. → https://www.uber.com/blog/michelangelo-machine-learning-platform/
- **Uber — Michelangelo: 2021+ evolution / Palette feature store** — how the platform matured. → https://www.uber.com/blog/tag/michelangelo/
- **Meta — FBLearner Flow** — reusable ML workflows at scale. → search "FBLearner Flow engineering Facebook"
- **Google — TFX: A TensorFlow-Based Production-Scale ML Platform** (paper) + docs. → https://www.tensorflow.org/tfx
- **Netflix — Metaflow** — human-friendly ML infrastructure (open source). → https://netflixtechblog.com/ and https://metaflow.org/
- **Spotify — ML platform (Hendrix / real-time ML)**. → https://engineering.atspotify.com/

## Feature stores
- **Feast** — the open-source feature store; docs explain online/offline stores and point-in-time joins. → https://docs.feast.dev/
- **Tecton** — managed feature platform; blog covers streaming features and training-serving consistency. → https://www.tecton.ai/blog/
- **Airbnb — Zipline / Chronon** (now open-sourced as **Chronon**) — point-in-time-correct features at scale. → https://github.com/airbnb/chronon
- **LinkedIn / Microsoft — Feathr** — enterprise feature store. → https://github.com/feathr-ai/feathr
- **DoorDash — building a feature store / gigascale ML**. → https://careersatdoordash.com/engineering-blog/
- **Reference:** *featurestore.org* — comparisons and patterns across implementations. → https://www.featurestore.org/

## Data engineering, quality & labeling
- **Great Expectations** — data validation/quality gates in pipelines. → https://greatexpectations.io/
- **DVC** and **LakeFS** — data/version control and git-like data-lake branching. → https://dvc.org/ · https://lakefs.io/
- **Snorkel — weak supervision / programmatic labeling** (research + product). → https://www.snorkel.org/
- **Google — Rules of Machine Learning (Martin Zinkevich)** — 43 timeless best-practice rules; excellent framing for interviews. → https://developers.google.com/machine-learning/guides/rules-of-ml

## Evaluation & experimentation
- **Netflix — It's All A/Bout Testing / experimentation platform** series. → https://netflixtechblog.com/tagged/experimentation
- **Microsoft (Kohavi et al.) — Trustworthy Online Controlled Experiments** — the A/B testing bible (book + KDD papers). → search "Trustworthy Online Controlled Experiments Kohavi"
- **Interleaving for ranking evaluation** (Netflix / academic). → search "interleaving evaluation ranking Netflix"
- **RAGAS** — evaluation framework for RAG pipelines (faithfulness, answer relevancy). → https://docs.ragas.io/
- **OpenAI Evals / LLM-as-judge patterns** — evaluating generative outputs. → https://github.com/openai/evals

## Model serving & inference
- **vLLM** — high-throughput LLM serving with PagedAttention / continuous batching. → https://docs.vllm.ai/
- **NVIDIA Triton Inference Server** — multi-framework serving, dynamic batching. → https://docs.nvidia.com/deeplearning/triton-inference-server/
- **TorchServe** / **TensorFlow Serving** — classic model servers. → https://pytorch.org/serve/ · https://www.tensorflow.org/tfx/guide/serving
- **Ray Serve / KServe** — scalable serving on Ray / Kubernetes. → https://docs.ray.io/en/latest/serve/ · https://kserve.github.io/website/

## MLOps, monitoring & drift
- **Evidently AI** — open-source data/model drift monitoring (referenced in the chapter). → https://docs.evidentlyai.com/
- **MLflow** — experiment tracking + model registry. → https://mlflow.org/docs/latest/
- **Google — MLOps: Continuous delivery and automation pipelines in ML** (MLOps levels 0–2). → https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning
- **Chip Huyen — *Designing Machine Learning Systems*** (book) + blog on data distribution shifts and monitoring. → https://huyenchip.com/

---

### Role-specific starting picks
| If you're interviewing as… | Read first |
|---|---|
| **ML engineer / DS** | Rules of ML (Google), Michelangelo, Chip Huyen's ML Systems |
| **MLOps / platform** | TFX, Feast docs, GCP MLOps levels, Evidently |
| **GenAI / applied LLM** | vLLM, RAGAS, RAG-eval + LLM-as-judge, feature/embedding + prompt-registry patterns |
| **Senior / staff (breadth)** | Michelangelo + Feast (feature-store contrast), Trustworthy A/B Experiments, MLOps levels |
