# Blog & Paper Index — Infrastructure, MLOps & Governance

Curated reading behind Chapter 8: **distributed training, GPU infrastructure & scheduling, ML platforms, LLM/agent observability, and AI governance (EU AI Act / NIST AI RMF)**. Papers cited by title; blog/framework links may drift.

> **Link maintenance:** if a link 404s, search the title. Last reviewed: 2026.

---

## Distributed training & GPU infrastructure
- **Megatron-LM** (Shoeybi et al.) — tensor/model parallelism for large transformers. → https://github.com/NVIDIA/Megatron-LM
- **ZeRO / DeepSpeed** (Rajbhandari et al.) — memory-optimized data parallelism (optimizer/gradient/parameter sharding); the "why data-parallel alone fails" fix. → https://github.com/deepspeedai/DeepSpeed
- **PyTorch FSDP (Fully Sharded Data Parallel)** — Meta's sharded data parallel. → https://engineering.fb.com/2021/07/15/open-source/fsdp/
- **GPipe** (Huang et al.) & **PipeDream** (Narayanan et al.) — pipeline parallelism with micro-batches. → search each by name
- **Efficient Large-Scale Language Model Training on GPU Clusters (Megatron 3D parallelism)** (Narayanan et al.) — combining data + tensor + pipeline parallelism. → search "Efficient large-scale language model training GPU clusters arXiv"
- **Ray** — distributed compute for training/serving orchestration. → https://github.com/ray-project/ray
- **NVIDIA collective comms / NCCL & NVLink/InfiniBand docs** — interconnects behind all-reduce. → https://developer.nvidia.com/nccl

## Scheduling & cluster management
- **Kubernetes** + **Kubeflow** — container orchestration for ML workloads. → https://www.kubeflow.org/
- **Slurm** — HPC scheduler common for training clusters. → https://slurm.schedmd.com/
- **Ray** (scheduling) and **Volcano** (batch scheduling on K8s). → https://volcano.sh/

## ML platforms (reference architectures)
- **Uber — Michelangelo**. → https://www.uber.com/blog/michelangelo-machine-learning-platform/
- **Google — TFX: A TensorFlow-Based Production-Scale ML Platform** (paper + docs). → https://www.tensorflow.org/tfx
- **Meta — FBLearner Flow**. → search "FBLearner Flow Facebook engineering"
- **Netflix — Metaflow**. → https://metaflow.org/
- (See the annotated tour in [`ml-platform-reference-architectures.md`](./ml-platform-reference-architectures.md).)

## Serving at scale (LLM & agents)
- **vLLM / PagedAttention** (Kwon et al.) — high-throughput serving. → https://docs.vllm.ai/
- **Orca** — continuous/iteration-level batching. → search "Orca continuous batching OSDI"
- **NVIDIA Triton Inference Server** — multi-framework production serving. → https://github.com/triton-inference-server
- **Temporal** — durable workflow orchestration (the model for stateful, long-running agent serving). → https://temporal.io/
- **AI gateways:** LiteLLM (https://github.com/BerriAI/litellm), Portkey, OpenRouter, Cloudflare AI Gateway, Kong AI Gateway.

## Observability & MLOps
- **Google — MLOps: Continuous delivery and automation pipelines in ML** (levels 0–2). → https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning
- **Chip Huyen — *Designing Machine Learning Systems*** + blog on data distribution shifts/monitoring. → https://huyenchip.com/
- **Evidently AI** — drift/quality monitoring. → https://docs.evidentlyai.com/
- **Agent/LLM observability:** Langfuse (https://langfuse.com/), Arize Phoenix, LangSmith, OpenLLMetry, OpenTelemetry (https://opentelemetry.io/).
- **Google SRE books** — SLIs/SLOs, error budgets, incident management. → https://sre.google/books/

## Responsible AI, fairness & explainability
- **A Survey on Bias and Fairness in Machine Learning** (Mehrabi et al.). → search title on arXiv
- **Fairlearn** (toolkit) & **AIF360** (IBM) — fairness metrics/mitigation. → https://fairlearn.org/ · https://aif360.res.ibm.com/
- **SHAP** (Lundberg & Lee) & **LIME** (Ribeiro et al.) — explainability. → https://github.com/shap/shap
- **Model Cards for Model Reporting** (Mitchell et al.) — the model-card standard (extended to *agent cards* in Ch. 8). → search "Model Cards for Model Reporting arXiv"
- **Datasheets for Datasets** (Gebru et al.). → search title

## Governance & regulation
- **EU AI Act** — official text/overview. → https://artificialintelligenceact.eu/
- **NIST AI Risk Management Framework (AI RMF 1.0)** — Govern/Map/Measure/Manage. → https://www.nist.gov/itl/ai-risk-management-framework
- **OECD AI Principles** — widely referenced policy baseline. → https://oecd.ai/
- **C2PA** — content provenance/authenticity standard. → https://c2pa.org/

---

### Role-specific starting picks
| If you're interviewing as… | Read first |
|---|---|
| **ML infra / training** | Megatron 3D-parallelism, ZeRO/DeepSpeed, FSDP, NCCL/NVLink |
| **MLOps / platform** | Michelangelo, TFX, GCP MLOps levels, Evidently |
| **GenAI / agent platform** | vLLM/PagedAttention, Temporal, AI gateways (LiteLLM), Langfuse |
| **Responsible AI / governance** | EU AI Act, NIST AI RMF, Model Cards, Fairlearn/AIF360 |
