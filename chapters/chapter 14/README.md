# Chapter 14 — Computer Vision

Companion resources for Chapter 14, anchored on **Google Lens-style visual search/recognition** with an on-device/edge thread. The recurring CV interview themes: **embeddings + ANN visual search**, **model architecture choices**, **OCR**, and the **on-device vs. cloud** split.

Chapter 14 covers CV architectures (CNN, ViT, YOLO, DETR, CLIP, SAM), visual search (image embeddings + ANN), OCR pipelines, self-supervised pretraining, transfer learning, edge deployment (quantization, distillation, split compute/cascade), and privacy.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 14 glossary slice (CLIP, ViT, YOLO, DETR, SAM, ANN, visual search, OCR, quantization, distillation, split compute, self-supervised pretraining, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — embeddings vs. classifiers, which architecture, OCR pipeline, on-device vs. cloud, latency, and where multimodal LLMs fit. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: Google Lens/visual search, CLIP/ViT/YOLO/SAM papers, ANN libraries, and mobile/edge model compression. |

> **How to use:** the highest-frequency CV interview task is **visual search** — be fluent in "embed the query → ANN over the index → rerank." Then layer architecture, OCR, and the edge split.
