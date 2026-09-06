# Common Interviewee Doubts — Chapter 14 (Computer Vision)

The questions candidates most often have about computer-vision rounds. Grouped by theme.

---

## Visual search (the most common task)

**1. How does visual search actually work?**
**Embed the query image → ANN search over an index of item embeddings → rerank with metadata.** A vision encoder (CNN/ViT/CLIP) maps images to vectors; nearest neighbors are visually similar items. This is the pattern to reach for whenever the prompt is "find similar / identify this."

**2. Classifier or embedding search for recognition?**
**Embedding + ANN search** when the label set is huge, open-vocabulary, or changes often (products, landmarks) — you add new items without retraining. A fixed **classifier** only for small, stable label sets. Interviewers probe this; defaulting to a giant softmax over millions of classes is a red flag.

**3. Why CLIP specifically?**
CLIP aligns image and text embeddings, so you get **text-to-image search** ("red running shoes") and **zero-shot** recognition without task-specific training. Mention it whenever open-vocabulary or multimodal query is useful.

## Architecture choices

**4. CNN or ViT?**
CNNs are efficient and strong with less data; **ViTs** shine at scale (lots of data/compute) and dominate many benchmarks. For edge, efficient CNNs (MobileNet/EfficientNet) or small ViTs. Justify by data scale and deployment target, not hype.

**5. Which detector — YOLO or DETR?**
**YOLO** for real-time/on-device detection (fast, one-stage). **DETR** for end-to-end transformer detection without anchors/NMS. Pick by the latency budget and whether you're on-device.

**6. When do I mention SAM / segmentation?**
When the task needs region masks (e.g., isolate the object before embedding, or model-assisted labeling). SAM is a promptable general segmenter worth naming.

## OCR

**7. Is OCR one model?**
No — it's a **pipeline**: text **detection** (find regions) → **recognition** (read characters) → layout/post-processing (and translation for Lens). Detection can run on-device. Metrics are **CER/WER**. Treating OCR as a single black box misses the design.

## On-device vs. cloud

**8. What runs on-device vs. in the cloud?**
On-device: latency/privacy-sensitive, light tasks (text/region detection, barcode, coarse classification) using **quantized/distilled** models. Cloud: large-index visual search and heavy recognition. The **split compute / cascade** pattern runs a fast on-device model and escalates hard cases to the cloud.

**9. How do I fit a model on a phone/glasses?**
**Quantization** (int8), **distillation** (small student from big teacher), efficient architectures (MobileNet), and pruning. Trade a little accuracy for big latency/size/power wins. Note the power/thermal/memory constraints explicitly.

## Data & training

**10. I don't have many labels — what do I do?**
**Self-supervised pretraining** (SimCLR/DINO/MAE) on unlabeled images + **transfer learning** (fine-tune a pretrained backbone). You almost never train from scratch. Use SAM/model-assisted labeling to scale annotation.

## Frontier & delivery

**11. Where do multimodal LLMs fit?**
For open-ended visual Q&A / reasoning ("what is this and how do I fix it?") layered on top of retrieval/recognition — ground answers in recognized entities. Mention as an extension, not a replacement for embeddings + ANN.

**12. How do I structure a CV answer under time pressure?**
Clarify (task, latency, on-device?) → for search: embeddings + ANN + rerank; for recognition/detection: pick architecture by latency/scale → OCR pipeline if text → **on-device/cloud split** with quantization/distillation → data strategy (pretraining/transfer) → metrics (top-k accuracy, mAP/IoU, CER/WER) + privacy. Lead with the visual-search pattern if the prompt is search/identify.
