# Key Terms — Chapter 6 (Foundation Model Systems: LLMs, RAG, Multimodal)

Interview-oriented definitions for the foundation-model vocabulary in Chapter 6. Each pairs a crisp definition with *why it matters* in a design round. Terms defined earlier (embedding, bi-/cross-encoder, quantization, feature store) are cross-referenced. Feeds the cumulative book glossary.

---

### Transformer & LLM internals
- **Transformer** — Neural architecture ("Attention Is All You Need", 2017) that processes a whole sequence at once via attention. *Why it matters:* the engine under every modern LLM; drives memory, latency, and cost.
- **Self-attention** — For each token, a weighted mix of all others via Query/Key/Value: `softmax(QKᵀ/√d)·V`. *Why it matters:* cost is **quadratic in sequence length**, which motivates KV caching and long-context tricks.
- **Positional encoding / RoPE** — How order is injected; rotary embeddings (RoPE) extrapolate to longer contexts better than sinusoidal/learned. *Why it matters:* underpins long-context support.
- **KV cache** — Cached key/value tensors for prior tokens, reused during generation; turns per-token attention from O(n²) to O(n). *Why it matters:* usually the **serving bottleneck** — it grows with batch × context × layers × hidden and caps batch size (sizing formula in Ch. 5).
- **Prefill vs decode** — Processing the prompt in parallel (prefill) vs generating tokens one-by-one (decode). *Why it matters:* prefill sets TTFT; decode sets TPS.
- **Context window** — Max tokens the model can attend to at once. *Why it matters:* bounds prompt + retrieved context; finite windows force truncation/compression.

### Customization approaches
- **Prompt engineering** — Steering the model via prompt design (zero-shot, few-shot, chain-of-thought, structured output). *Why it matters:* cheapest, fastest; the default first move.
- **Chain-of-thought (CoT)** — Prompting the model to reason step-by-step. *Why it matters:* helps complex reasoning at the cost of tokens/latency.
- **Fine-tuning** — Further training a base model on task data to change **behavior** (style, format, instruction-following). *Why it matters:* the answer when prompting can't get consistent behavior.
- **LoRA / QLoRA** — Low-rank adapters (train ~0.1–1% of params); QLoRA runs on a 4-bit base. *Why it matters:* cheap fine-tuning on modest hardware; the practical default.
- **RLHF / DPO** — Aligning outputs to human preferences via a reward model (RLHF) or directly from preference pairs (DPO). *Why it matters:* improves helpfulness/harmlessness beyond task accuracy.
- **RAG (Retrieval-Augmented Generation)** — Retrieve relevant docs at inference and condition generation on them. *Why it matters:* changes **what the model knows** — fresh/private/citable knowledge without retraining; reduces hallucination.

### LLM serving & inference optimization
- **Continuous batching** — Admitting new requests as others finish instead of fixed batches. *Why it matters:* big throughput/utilization win; raises concurrent streams per GPU.
- **Paged attention** — Storing KV cache in non-contiguous pages (popularized by vLLM). *Why it matters:* cuts memory fragmentation and enables much larger batches on the same GPU.
- **Speculative decoding** — A small draft model proposes tokens; the large model verifies them in parallel. *Why it matters:* higher token throughput with no quality loss when the draft is accurate.
- **Model routing** — A lightweight classifier sends simple queries to a small model, hard ones to a large model. *Why it matters:* cuts cost with little quality impact.
- **Model cascade** — Try a small model first; escalate to a larger one only on low confidence/failed checks. *Why it matters:* most requests stay cheap.
- **Semantic / prompt / session caching** — Reuse responses for similar queries, reuse computation for shared prompt prefixes, reuse KV across conversation turns. *Why it matters:* major latency and cost reductions.
- **Spot / preemptible GPUs** — Discounted interruptible instances. *Why it matters:* good for batch inference, unsafe for latency-critical online serving.

### Latency metrics (LLM UX)
- **TTFT (Time-to-First-Token)** — Delay until the first output token. *Why it matters:* dominates *perceived* responsiveness in chat; driven by prefill.
- **TPS (Tokens-per-Second)** — Generation rate after the first token. *Why it matters:* determines streaming smoothness and concurrent-stream capacity.
- **End-to-end latency** — Total submit-to-complete time. *Why it matters:* the key metric for non-streaming/batch use cases.
- **Streaming responses (SSE)** — Push tokens to the client as generated. *Why it matters:* hides latency; the standard chat UX.

### RAG pipeline
- **Chunking** — Splitting documents into retrievable units (fixed, sentence, semantic, recursive, structure-aware). *Why it matters:* a high-impact, often-overlooked decision; ~512 tokens with 10–20% overlap is a common start.
- **Hybrid search** — Combining keyword (BM25) and vector search. *Why it matters:* keyword nails exact terms (IDs, codes); vectors catch semantics.
- **Reciprocal Rank Fusion (RRF)** — Merging ranked lists from multiple retrievers. *Why it matters:* the standard way to fuse hybrid-search results before reranking.
- **HNSW** — Graph-based approximate nearest-neighbor index for vector search. *Why it matters:* the workhorse ANN index; fast recall at scale (with ~1.5× storage overhead — Ch. 5).
- **Reranker (cross-encoder)** — Second stage that jointly scores query + each candidate. *Why it matters:* often the single **highest-impact** improvement over plain vector search.
- **HyDE (Hypothetical Document Embeddings)** — Embed an LLM-generated hypothetical answer for retrieval. *Why it matters:* helps when query and document wording differ.
- **Query transformation** — Expansion, decomposition, step-back prompting to improve retrieval. *Why it matters:* fixes recall on short/ambiguous/multi-part queries.
- **MMR (Maximal Marginal Relevance)** — Selects results that are relevant *and* diverse. *Why it matters:* reduces redundant context, enriching what the LLM sees.
- **Metadata filtering** — Restricting retrieval by source, date, language, tenant, permissions. *Why it matters:* relevance + access control.
- **Advanced RAG (Adaptive / Corrective / Self-RAG / Multi-hop / GraphRAG / Agentic)** — Patterns that decide when/what to retrieve, grade retrieval, or reason across sources. *Why it matters:* add only when the problem demands it — they raise complexity, latency, and cost.

### Evaluation & safety
- **RAG evaluation levels** — Retrieval (Recall@K, MRR, NDCG), generation (faithfulness, relevance, completeness), end-to-end (answer correctness, hallucination rate, citation accuracy). *Why it matters:* evaluate retrieval and generation **separately** to locate failures.
- **Faithfulness / groundedness** — Whether the answer is supported by retrieved context. *Why it matters:* the core anti-hallucination metric for RAG.
- **RAGAS / TruLens / DeepEval** — Frameworks that automate RAG/LLM evaluation with LLM-based metrics. *Why it matters:* scalable eval, but calibrate against human judgment.
- **LLM-as-a-Judge** — Using a stronger model to score outputs. *Why it matters:* scales evaluation but has biases (e.g., favoring verbosity) — calibrate.
- **Benchmarks (MMLU, HumanEval, GSM8K, TruthfulQA, HELM)** — Standard capability probes. *Why it matters:* coarse comparators, not predictors of app performance.
- **Hallucination** — Plausible but false model output. *Why it matters:* mitigate with RAG, low temperature, source attribution, and abstention; detect via fact-checking/self-consistency.
- **Guardrails** — Input filters (harmful content, prompt injection, jailbreaks) and output filters (PII, policy, unsafe content). *Why it matters:* production LLMs need both; pair with red teaming.
- **Prompt injection / jailbreak** — Malicious input that overrides system instructions. *Why it matters:* a core LLM-native threat; sanitize outputs before executing/storing them.
- **Red teaming** — Systematically probing with adversarial prompts before launch. *Why it matters:* surfaces vulnerabilities proactively.

### Multimodal
- **Multimodal model** — Processes/generates across text, image, audio, video in one architecture. *Why it matters:* increasingly the default for VQA, document, and media tasks.
- **Fusion (early / late / cross-attention)** — Combining modalities before the backbone / at the decision stage / via attention across modalities. *Why it matters:* trade-off between rich interaction and modularity/cost.
- **VLM (Vision-Language Model)** — Image encoder + LLM (e.g., captioning, VQA, doc/chart understanding). *Why it matters:* extends LLM design with a vision encoder + alignment layers.
- **Multimodal embedding (CLIP, ImageBind)** — Projects modalities into a shared space for cross-modal retrieval. *Why it matters:* enables "search images with text" and multimodal RAG.
- **Multimodal RAG** — Retrieval over text + images/tables/charts, answered by a VLM. *Why it matters:* handles enterprise knowledge that text-only RAG can't.
- **OCR + NLP vs layout-aware models (LayoutLM, Donut)** — Extract-then-reason pipeline vs models that use text + 2D layout (or raw pixels). *Why it matters:* the two document-understanding architectures; discuss OCR quality, validation, and human-in-the-loop.
- **Generation quality metrics (FID, CLIP Score, WER)** — Image realism/alignment, prompt alignment, speech recognition error. *Why it matters:* each modality needs its own metric, complemented by human eval.
- **Watermarking / provenance** — Embedding traceability metadata in generated media. *Why it matters:* content authenticity and abuse mitigation for generative systems.

---

*Cross-refs:* embedding, bi-/cross-encoder, quantization/distillation, canary/shadow, drift → Chapter 4. GPU memory, KV-cache sizing, TTFT/TPS, arithmetic intensity, FLOPs → Chapter 5. Vector DB, caching, CDN, rate limiting, API gateway → Chapter 3.
