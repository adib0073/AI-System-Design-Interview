# Key Terms — Chapter 14 (Computer Vision)

Interview-oriented definitions for the vocabulary in Chapter 14 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Architectures
- **Vision Transformer (ViT)** — Transformer architecture for images. *Why it matters:* strong with large data/scale; the modern alternative to CNN backbones.
- **YOLO** — A fast one-stage object detector. *Why it matters:* well-suited to real-time/on-device detection; the go-to when latency dominates.
- **DETR** — Transformer-based object detector. *Why it matters:* end-to-end detection without hand-designed anchors/NMS; cite as the transformer detection option.
- **CLIP** — Image–text contrastive model producing aligned embeddings. *Why it matters:* enables **text-to-image search** and **zero-shot** recognition; the backbone of open-vocabulary visual search.
- **SAM (Segment Anything Model)** — Meta's promptable, general segmentation model. *Why it matters:* general-purpose segmentation and model-assisted labeling.

### Visual search & representations
- **Visual search** — Retrieving visually similar items via image embeddings + ANN, optionally region-based and text-to-image. *Why it matters:* the most common CV interview task (Lens, product search).
- **Embedding (visual)** — A dense vector representing an image (or region). *Why it matters:* the unit of similarity/retrieval; embed once, reuse.
- **ANN (Approximate Nearest Neighbor)** — Index (ScaNN/FAISS/HNSW) for fast similarity retrieval over image embeddings. *Why it matters:* makes billion-image visual search sub-second; scales far better than a fixed-class classifier.
- **Self-supervised pretraining** — Learning features from unlabeled images (SimCLR/DINO/MAE). *Why it matters:* reduces labeling needs; leverages abundant unlabeled data.
- **Transfer learning** — Fine-tuning a pretrained backbone for a new task instead of training from scratch. *Why it matters:* the default; you rarely train CV models from zero.

### OCR & metrics
- **OCR (Optical Character Recognition)** — Detecting and reading text in images; pipeline of detection → recognition → layout. *Why it matters:* a distinct sub-pipeline (Lens translate, document AI); don't treat as a single model.
- **CER / WER** — Character/word error rate. *Why it matters:* the OCR recognition metrics to name.
- **mAP / IoU** — Mean average precision / intersection-over-union. *Why it matters:* the object-detection and segmentation metrics.

### Edge deployment
- **Edge / on-device inference** — Running models on the phone/glasses. *Why it matters:* latency, privacy, offline use, and cost — but bounded by power/memory/thermal; a core CV design trade-off.
- **Quantization** — Reducing numeric precision (e.g., int8) to shrink/speed up models. *Why it matters:* the primary lever to fit models on-device with modest accuracy loss.
- **Distillation** — Training a small "student" from a large "teacher." *Why it matters:* fits edge constraints with less accuracy loss than training small from scratch.
- **Split compute / cascade** — Fast model on-device, escalate hard cases to a heavier cloud model. *Why it matters:* the on-device/cloud latency-privacy-accuracy balance in one pattern.

---

*Cross-refs:* embeddings, ANN, RAG-adjacent retrieval → Ch. 6/9. Multimodal LLMs → Ch. 6. Serving/latency/cost → Ch. 3/5. Storefront/Lens case studies → mock problems 05 & 08.
