# Engineering Blogs & Papers — Chapter 14 (Computer Vision)

Curated, interview-relevant reading. Focus on *retrieval + deployment* design (embeddings/ANN, edge), not just SOTA benchmarks. Search titles if links move.

## Start here (highest signal)
- **CLIP: "Learning Transferable Visual Models from Natural Language Supervision"** (Radford et al., OpenAI, 2021) — image–text embeddings, zero-shot, text-to-image search. Read first.
- **Google "Lens / visual search"** engineering & product posts — the anchor use case: embeddings + ANN + OCR + on-device.
- **ScaNN** (Google) / **FAISS** (Meta) — the ANN libraries; understand IVF-PQ vs. HNSW trade-offs.

## Architectures
- **ResNet** (He et al., 2015) — the CNN backbone baseline.
- **ViT: "An Image is Worth 16x16 Words"** (Dosovitskiy et al., 2020) — transformers for vision.
- **YOLO** series (Redmon et al. and successors) — real-time one-stage detection.
- **DETR** (Carion et al., Meta, 2020) — end-to-end transformer detection.
- **SAM: "Segment Anything"** (Kirillov et al., Meta, 2023) — promptable segmentation.

## Self-supervised & representation learning
- **SimCLR** (Chen et al., 2020), **DINO / DINOv2** (Meta), **MAE** (He et al., 2021) — learning from unlabeled images.

## Visual search systems
- **Pinterest visual search / "Lens"** posts — embeddings + ANN + reranking at product scale.
- **Amazon / e-commerce visual search** write-ups — region-based product retrieval.

## OCR
- **Tesseract** and modern deep OCR write-ups — detection → recognition → layout pipeline.
- **TrOCR / PaddleOCR** — transformer/production OCR references.

## Edge / on-device
- **MobileNet** (Howard et al.) and **EfficientNet** (Tan & Le) — efficient backbones.
- **Model quantization & distillation** guides (TensorFlow Lite, PyTorch Mobile, Core ML) — fitting models on device.
- **"Distilling the Knowledge in a Neural Network"** (Hinton et al., 2015) — the distillation classic.

## How to use in prep
1. Read the CLIP paper and one Lens/Pinterest visual-search post — that covers embeddings + ANN + open-vocabulary.
2. Be able to name a detector (YOLO/DETR) and a backbone (ResNet/ViT) with the trade-off.
3. Have the **quantization + distillation + split-compute** edge story ready.
4. Prepare the **OCR as a pipeline** answer (detection → recognition → layout).
