# Prompt vs. Fine-tune vs. RAG — Decision Matrix (Printable)

One page to answer the single most common LLM system design question: *"Would you prompt, fine-tune, or use RAG?"* The honest answer is usually **"start with prompting, add RAG for knowledge, fine-tune for behavior — and combine them."**

---

## The one-line rule
- **Prompting** — the model *can* do it; you just need to ask well. → cheapest, start here.
- **RAG** — the model needs *knowledge it doesn't have* (fresh, private, verifiable). → changes **what it knows**.
- **Fine-tuning** — the model needs to *behave differently* (style, format, domain tone, instruction-following). → changes **how it behaves**.

## Decision flow
```
Is the task within the base model's capability, no external/private facts needed?
├─ YES → PROMPT ENGINEERING (zero/few-shot, CoT, structured output). Iterate here first.
└─ NO → Does it need dynamic / proprietary / large / citable knowledge?
        ├─ YES → RAG (retrieve → rerank → generate, with citations).
        └─ Is the gap about BEHAVIOR (style, tone, format, instruction-following, domain jargon)?
                 ├─ YES → FINE-TUNE (LoRA/QLoRA first; full FT rarely).
                 └─ Brand-new language / modality / architecture? → TRAIN FROM SCRATCH (rare).

Common production answer = RAG (knowledge) + light fine-tune (behavior).
```

## Comparison matrix
| Dimension | Prompt engineering | RAG | Fine-tuning |
|---|---|---|---|
| **Changes** | Nothing (input only) | What the model *knows* | How the model *behaves* |
| **Best for** | Tasks in-capability; fast iteration | Fresh/private/large knowledge; citations | Style, tone, format, instruction-following, domain jargon |
| **Knowledge freshness** | Model cutoff | Real-time (re-index) | Frozen at train time |
| **Hallucination control** | Weak | Strong (grounded + citable) | Medium |
| **Upfront cost/effort** | Lowest | Medium (retrieval infra) | High (data + compute) |
| **Per-request cost** | Base (grows with prompt size) | Base + retrieval + longer context | Base (can shrink prompts) |
| **Latency** | Base | + retrieval/rerank | Base |
| **Data needed** | 0–few examples | A document corpus | 100s–10K+ labeled examples |
| **Ops complexity** | Minimal | Vector DB, indexing, eval pipeline | Training + serving the adapted model |
| **Updates by** | Editing the prompt | Updating the index | Retraining |

## Prompt-engineering techniques (the cheap wins first)
| Technique | Use when | Cost |
|---|---|---|
| **Zero-shot** | Straightforward tasks | Lowest |
| **Few-shot (1–5 examples)** | Need consistent format/accuracy | + input tokens |
| **Chain-of-thought** | Multi-step reasoning/math/logic | + tokens + latency |
| **Structured output (JSON/schema)** | Downstream needs to parse it | + validation/retry |

## Fine-tuning methods (cheapest adaptation first)
| Method | Trains | When |
|---|---|---|
| **LoRA** | ~0.1–1% of params (adapters) | Default task adaptation; cheap, strong |
| **QLoRA** | LoRA on a 4-bit base | Fine-tune a big model on one GPU |
| **Adapters** | ~1–4% (inserted modules) | Multi-task; swap adapters without retraining |
| **Full fine-tune** | All params | Large domain shift, new capability; costly (10K+ examples) |
| **RLHF / DPO** | Alignment to preferences | Improve *behavior* from human preference data |

## When to combine
- **RAG + fine-tune:** fine-tune for house style/format, RAG for up-to-date facts + citations. (Most common enterprise pattern.)
- **RAG + prompting:** the default for knowledge assistants; no training at all.
- **Fine-tune to shrink prompts:** if a giant few-shot prompt is expensive at scale, distill it into a fine-tune.

## Interview red flags → say this instead
| Red flag | Better move |
|---|---|
| "I'd fine-tune it" (for a knowledge problem) | RAG — fine-tuning doesn't add fresh/verifiable facts |
| "I'd use RAG" (for a tone/format problem) | Fine-tune (or a stronger system prompt) — RAG doesn't change behavior |
| Jumping to training from scratch | Almost never justified; start from a foundation model |
| Ignoring evaluation | Evaluate retrieval and generation *separately*, then end-to-end |

---

*See also:* [`../chapter 4/decision-trees-checklists.md`](../chapter%204/decision-trees-checklists.md) for the broader model-selection tree, and [`blog-paper-index.md`](./blog-paper-index.md) for RAG technique deep-dives (HyDE, ColBERT, RAGAS).
