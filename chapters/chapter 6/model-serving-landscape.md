# Model & Serving Landscape — Living Reference

A fast-moving snapshot of **serving frameworks, model families, and rough pricing** for LLM system design. This lives in the repo (not the book) precisely because it goes stale quickly.

> ⚠️ **This page is volatile.** Model versions, context windows, and prices change monthly. Treat every number as *order-of-magnitude* and **verify against the provider before quoting in an interview or design.** Last reviewed: 2026. In an interview, reason about *categories and trade-offs* rather than memorizing versions.

---

## 1. Serving frameworks

| Framework | Best for | Key features | Notes |
|---|---|---|---|
| **vLLM** | High-throughput open-model serving | PagedAttention, continuous batching, prefix caching, OpenAI-compatible API | The default open-source choice for throughput. → https://docs.vllm.ai/ |
| **TGI (Text Generation Inference)** | Hugging Face ecosystem serving | Continuous batching, quantization, tensor parallelism | Tight HF Hub integration. → https://github.com/huggingface/text-generation-inference |
| **TensorRT-LLM** | Max performance on NVIDIA GPUs | Compiled kernels, FP8, in-flight batching | Fastest on NVIDIA but heavier build/setup. → https://github.com/NVIDIA/TensorRT-LLM |
| **SGLang** | Structured generation, complex prompting | RadixAttention (prefix reuse), fast structured decoding | Strong for agent/tool and JSON workloads. → https://github.com/sgl-project/sglang |
| **NVIDIA Triton** | Multi-framework production serving | Dynamic batching, multi-model, backends incl. TRT-LLM | General-purpose server, not LLM-only. → https://github.com/triton-inference-server |
| **Ollama / llama.cpp** | Local / edge / CPU / laptop | GGUF quantized models, tiny footprint | Great for prototyping and on-device. → https://ollama.com/ · https://github.com/ggml-org/llama.cpp |
| **Ray Serve / KServe** | Orchestration & autoscaling | Scale serving on Ray / Kubernetes | Wrap the engines above for scale-out. |

**Framework selection heuristic:** open-weight + throughput → **vLLM**; deepest NVIDIA optimization → **TensorRT-LLM**; HF-centric → **TGI**; heavy structured/agent output → **SGLang**; local/edge → **Ollama/llama.cpp**; managed API → skip all of this and call a provider.

## 2. Open-weight model families
Self-hostable; fine-tune freely; run in your VPC or on edge. Sizes/versions change constantly.

| Family | Vendor | Typical sizes | Notes |
|---|---|---|---|
| **Llama** | Meta | ~1B–400B (dense & MoE) | Broadest ecosystem/tooling support |
| **Qwen** | Alibaba | ~0.5B–200B+; VL variants | Strong multilingual + vision-language |
| **Mistral / Mixtral** | Mistral AI | ~7B dense, MoE variants | Efficient MoE, permissive licenses |
| **Gemma** | Google | ~2B–27B | Lightweight, good for edge |
| **DeepSeek** | DeepSeek | large MoE, reasoning variants | Strong reasoning/coding at low cost |
| **Phi** | Microsoft | ~2B–14B | "Small but capable"; edge-friendly |

**Sizing heuristic (from §6.1):** 1–8B → edge/mobile, classification, extraction, simple agents (single/quantized GPU). 13–34B → general chat, mid-quality RAG, code assistants (single 80 GB GPU, quantized). 70B+ dense/MoE → highest quality, multi-GPU; use only when quality justifies cost.

## 3. Proprietary (hosted API) models
Managed inference; best-in-class capability; pay per token; data leaves your VPC (unless enterprise/private endpoints).

| Family | Vendor | Access | Use when |
|---|---|---|---|
| **GPT** | OpenAI | API | Frontier capability, tool/vision, fast prototyping |
| **Claude** | Anthropic | API | Long context, careful reasoning, coding |
| **Gemini** | Google | API | Multimodal, long context, GCP integration |

**Open vs proprietary (from §6.1):** proprietary for prototyping or when capability is the bottleneck; open-weight when cost-at-scale, privacy, or full control dominate. Regulated industries often mandate open-weight or private-cloud endpoints.

## 4. Pricing — how to reason (not memorize)
Prices change constantly and differ by model tier, so learn the **shape**, not the digits:

- **Hosted APIs** bill per **million tokens**, with **input cheaper than output**, and separate (higher) tiers for frontier/reasoning models. Cheap "mini/flash/small" tiers can be 10–50× cheaper than flagship tiers.
- **Self-hosting** cost ≈ **GPU-hours × $/GPU-hr ÷ tokens served**. It wins over APIs only at **high, steady utilization** — an idle GPU is pure cost.
- **Rough cloud GPU rates (verify!):** A100 80GB ≈ $1.5–4/hr, H100 80GB ≈ $2–5/hr on-demand; **spot/preemptible ≈ 60–70% cheaper**.
- **Break-even mental model:** estimate tokens/day → API cost/day vs. (GPUs needed × $/hr × 24). Below break-even volume, APIs are cheaper *and* simpler.

Use the [`../chapter 5/estimation-calculators.ipynb`](../chapter%205/estimation-calculators.ipynb) `training_cost` / GPU-memory helpers to sketch these quickly.

## 5. Cost / latency optimizations (recap from §6.3)
Model routing · model cascades (small model first, escalate on low confidence) · quantization (FP16→INT8/FP8/INT4) · continuous batching · speculative decoding · paged attention · semantic + prompt (prefix) + per-session KV caching · spot GPUs for batch workloads.

---

### Maintaining this page
This is intentionally a living document. When a major model or framework ships, update the tables and bump the "Last reviewed" date. **Do not** put these volatile specifics in the book — link here instead. Corrections welcome via issue/PR.
