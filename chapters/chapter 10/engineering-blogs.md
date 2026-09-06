# Engineering Blogs & Papers — Chapter 10 (Ads Ranking & Computational Advertising)

Curated, interview-relevant reading. Focus on *why* (auction choice, calibration, delayed feedback), not memorizing model layers. Search titles if links move.

> **Living note:** privacy (ATT, Privacy Sandbox) is actively evolving — treat those entries as directional and check current status before quoting specifics.

## Start here (highest signal)
- **"Ad Click Prediction: a View from the Trenches"** (McMahan et al., Google, KDD 2013) — the classic practical CTR-prediction paper (FTRL, calibration, feature hashing). Read first.
- **ESMM: "Entire Space Multi-Task Model"** (Ma et al., Alibaba, SIGIR 2018) — solves **click-only selection bias** for pCVR. The must-cite CVR paper.
- **"Delayed Feedback Model"** (Chapelle, Criteo, 2014) — training conversion models with delayed labels.

## Auctions & mechanism design
- Overviews of **GSP, second-price/Vickrey, and VCG** (e.g., Tim Roughgarden's lecture notes / AGT texts) — intuition, not proofs.
- **Facebook/Meta VCG-style auctions** engineering discussions — why a truthful multi-slot mechanism.
- **First-price auctions & bid shading in RTB** — industry write-ups on the exchange move to first-price.

## CTR / CVR modeling
- **Wide & Deep** (Cheng et al., Google, 2016) and **DCN / DCN-v2** (Google) — feature crosses for CTR.
- **DeepFM** (Guo et al., 2017) — factorization machines + deep.
- **Practical Lessons from Predicting Clicks on Ads at Facebook** (He et al., 2014) — GBDT + logistic, calibration in practice.

## Calibration
- **Platt scaling** and **isotonic regression** references — post-hoc calibration methods.
- Calibration-in-recommender/ads write-ups — why ranking metrics aren't enough when scores set prices.

## Real-world systems (design blogs)
- **Meta / Facebook Ads** engineering posts — value model, VCG auction, and delivery.
- **Google Ads / Ad Rank** documentation — bid × quality × context; auto-bidding (tCPA/tROAS/Max Conversions).
- **Pinterest, Twitter, and Criteo** ads engineering blogs — retrieval → ranking → auction at scale.
- **Budget pacing** posts (e.g., Yahoo/LinkedIn/Meta) — pacing as a feedback-control problem.

## Privacy-preserving advertising
- **Apple App Tracking Transparency (ATT)** — the signal-loss trigger.
- **Google Privacy Sandbox** — Topics API, Protected Audience, **Attribution Reporting** (aggregated, on-device).
- Write-ups on **modeled/aggregated conversions** post-signal-loss.

## How to use in prep
1. Read the Google "Trenches" paper and ESMM — they anchor CTR prediction, calibration, and CVR bias.
2. Be able to write the **eCPM formula** and explain **why calibration matters** in one breath.
3. Know one auction (second-price → GSP → VCG) well enough to explain truthfulness.
4. Have a one-paragraph take on **Privacy Sandbox / ATT** for senior rounds.
