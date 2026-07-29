# Chapter 6 — Foundation Model Systems: LLMs, RAG, and Multimodal AI

Companion resources for Chapter 6. Maintained here (not in the printed book) so they can be kept current — especially the fast-moving model/serving landscape.

Chapter 6 covers foundation-model systems end-to-end: transformer/LLM internals, the prompt/fine-tune/RAG decision, LLM serving & inference optimization, production RAG, and multimodal AI.

| File | What it is |
|------|------------|
| [`prompt-finetune-rag-matrix.md`](./prompt-finetune-rag-matrix.md) | Printable decision matrix for the #1 LLM interview question: prompt vs. fine-tune vs. RAG — with a decision flow, comparison table, technique tables, and red-flag fixes. |
| [`model-serving-landscape.md`](./model-serving-landscape.md) | **Living reference** (volatile → repo only): serving frameworks (vLLM/TGI/TensorRT-LLM/SGLang), open-weight & proprietary model families, and how to *reason* about pricing. Verify before quoting. |
| [`blog-paper-index.md`](./blog-paper-index.md) | Papers & write-ups behind the chapter: transformers/serving (PagedAttention, speculative decoding), retrieval/reranking (ColBERT, RRF), RAG techniques (HyDE, Self-RAG, GraphRAG), and evaluation (RAGAS). |
| [`key-terms.md`](./key-terms.md) | Chapter 6 glossary slice (KV cache, continuous batching, paged attention, HNSW, reranker, HyDE, hallucination, guardrails, multimodal fusion, …). Feeds the cumulative book glossary. |

> **Note on links:** model versions and prices change monthly — `model-serving-landscape.md` is intentionally a living document. If a link is dead, search the title or open an issue/PR.
