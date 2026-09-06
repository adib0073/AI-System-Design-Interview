# Chapter 15 — Forecasting & Prediction

Companion resources for Chapter 15, anchored on **demand forecasting**. The two ideas that dominate forecasting interviews: **no temporal leakage** (point-in-time features + rolling-origin backtesting) and **global vs. local models**.

Chapter 15 covers time-series features (lags, rolling stats, calendar) without leakage, global vs. local models, probabilistic/quantile forecasting (DeepAR, TFT), rolling-origin backtesting, WAPE/MASE metrics, hierarchical reconciliation, cold start, intermittent demand, and forecasting foundation models.

| File | What it is |
|------|------------|
| [`key-terms.md`](./key-terms.md) | Chapter 15 glossary slice (backtesting, temporal leakage, global vs. local, probabilistic forecast, pinball loss, WAPE/MASE, seasonal naive, newsvendor, DeepAR/TFT, Croston, …). Scanned from the chapter. Feeds the cumulative glossary. |
| [`common-doubts.md`](./common-doubts.md) | The questions candidates most often have — avoiding leakage, global vs. local, point vs. probabilistic, backtesting, metric choice, cold start, and intermittent demand. |
| [`engineering-blogs.md`](./engineering-blogs.md) | Curated reading: DeepAR/TFT, M-competitions, Uber/Amazon/Meta forecasting, and foundation forecasting models. |

> **How to use:** if you say only two things well, make them **"no leakage, validate with rolling-origin backtesting"** and **"one global model across series, not one per series."** Those anchor every forecasting round.
