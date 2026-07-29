# Blog & Paper Index — Foundation Models, RAG & Serving

Curated papers and write-ups behind Chapter 6: **transformer/serving internals, RAG techniques, retrieval/reranking, and evaluation**. Papers are cited by title (durably findable); blog/tool links may drift.

> **Link maintenance:** if a link 404s, search the title. Papers are on arXiv. Last reviewed: 2026.

---

## Transformers & attention (foundations)
- **Attention Is All You Need** (Vaswani et al., 2017) — the original transformer. → search "Attention Is All You Need arXiv"
- **RoFormer: Rotary Position Embedding (RoPE)** (Su et al.) — the positional encoding in modern LLMs. → search "RoFormer RoPE arXiv"
- **FlashAttention / FlashAttention-2** (Dao et al.) — IO-aware exact attention; why long context got cheaper. → search "FlashAttention arXiv"

## LLM serving & inference optimization
- **Efficient Memory Management for LLM Serving with PagedAttention** (Kwon et al., 2023) — the **vLLM** paper; KV cache as paged memory. → search "PagedAttention vLLM arXiv"
- **Orca: A Distributed Serving System for Transformer-Based Generative Models** — introduced **continuous (iteration-level) batching**. → search "Orca continuous batching OSDI"
- **Fast Inference from Transformers via Speculative Decoding** (Leviathan et al.) — draft-then-verify decoding. → search "Speculative Decoding arXiv"
- **vLLM blog & docs** — practical serving guidance. → https://blog.vllm.ai/ · https://docs.vllm.ai/

## Retrieval, embeddings & reranking
- **Dense Passage Retrieval (DPR)** (Karpukhin et al.) — the bi-encoder retrieval baseline. → search "Dense Passage Retrieval arXiv"
- **ColBERT** and **ColBERTv2** (Khattab & Zaharia; Santhanam et al.) — late-interaction retrieval; strong recall/precision balance. → https://github.com/stanford-futuredata/ColBERT
- **BM25 / Reciprocal Rank Fusion (RRF)** — keyword retrieval + hybrid-search fusion. → search "Reciprocal Rank Fusion Cormack"
- **Sentence-BERT (SBERT)** — practical sentence embeddings + cross-encoder rerankers. → https://www.sbert.net/
- **MTEB (Massive Text Embedding Benchmark)** — how to compare embedding models. → https://huggingface.co/spaces/mteb/leaderboard

## RAG — core & query techniques
- **Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks** (Lewis et al., 2020) — the original RAG paper. → search "Retrieval-Augmented Generation Lewis 2020 arXiv"
- **HyDE — Precise Zero-Shot Dense Retrieval without Relevance Labels** (Gao et al.) — hypothetical-document embeddings. → search "HyDE Hypothetical Document Embeddings arXiv"
- **Step-Back Prompting (Take a Step Back)** (Zheng et al.) — abstract the query before retrieving. → search "Take a Step Back prompting arXiv"
- **Self-RAG** (Asai et al.) — model decides when to retrieve and critiques itself. → search "Self-RAG arXiv"
- **Corrective RAG (CRAG)** (Yan et al.) — grade retrieved docs, correct on low quality. → search "Corrective RAG CRAG arXiv"
- **GraphRAG** (Microsoft Research) — graph-structured retrieval for global/relationship questions. → https://microsoft.github.io/graphrag/
- **MMR — Maximal Marginal Relevance** (Carbonell & Goldstein) — diversity in retrieved context. → search "Maximal Marginal Relevance Carbonell"

## RAG & LLM evaluation
- **RAGAS: Automated Evaluation of Retrieval Augmented Generation** — faithfulness, answer/context relevancy metrics. → https://docs.ragas.io/ · search "RAGAS arXiv"
- **TruLens** — feedback functions / RAG triad (context relevance, groundedness, answer relevance). → https://www.trulens.org/
- **DeepEval** — unit-testing-style LLM/RAG evaluation. → https://github.com/confident-ai/deepeval
- **LLM-as-a-Judge** (e.g., MT-Bench / Zheng et al.) — using a strong model to score outputs, with bias caveats. → search "Judging LLM-as-a-Judge MT-Bench arXiv"
- **Benchmarks:** MMLU, HumanEval, GSM8K, TruthfulQA, HELM — capability probes; treat as coarse indicators. → search each by name.

## Fine-tuning & alignment
- **LoRA: Low-Rank Adaptation of Large Language Models** (Hu et al.). → search "LoRA Low-Rank Adaptation arXiv"
- **QLoRA: Efficient Finetuning of Quantized LLMs** (Dettmers et al.). → search "QLoRA arXiv"
- **InstructGPT / RLHF** (Ouyang et al.) and **Direct Preference Optimization (DPO)** (Rafailov et al.) — alignment methods. → search each by name.

## Multimodal
- **CLIP — Learning Transferable Visual Models from Natural Language Supervision** (Radford et al.). → search "CLIP OpenAI arXiv"
- **ImageBind** (Meta) — one embedding space across modalities. → search "ImageBind arXiv"
- **LayoutLM / Donut** — document understanding with/without OCR. → search "LayoutLM arXiv" · "Donut OCR-free document understanding arXiv"

---

### Role-specific starting picks
| If you're interviewing as… | Read first |
|---|---|
| **Applied LLM / GenAI engineer** | RAG (Lewis 2020), PagedAttention, RAGAS, HyDE, LoRA/QLoRA |
| **Search / retrieval engineer** | DPR, ColBERTv2, RRF/hybrid search, MMR, MTEB |
| **Infra / serving** | PagedAttention (vLLM), Orca (continuous batching), Speculative Decoding, FlashAttention |
| **Senior / staff (breadth)** | Attention Is All You Need, RAG, PagedAttention, Self-RAG/CRAG, RAGAS |
