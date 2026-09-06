# Key Terms — Chapter 15 (Forecasting & Prediction)

Interview-oriented definitions for the vocabulary in Chapter 15 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Validation & leakage (the crux)
- **Backtesting (rolling-origin / walk-forward)** — Time-based evaluation that trains on the past and tests on the following horizon, rolling forward. *Why it matters:* the **correct** time-series validation; random k-fold leaks the future and inflates metrics.
- **Leakage (temporal)** — Using future information (via random splits or non-point-in-time features) that won't exist at prediction time. *Why it matters:* the #1 forecasting mistake; inflates offline metrics and collapses in production.
- **Horizon** — How far ahead you forecast. *Why it matters:* different horizons are different problems (next-day vs. next-quarter need different features/models).

### Models
- **Global vs. local model** — One model trained across all series (scalable, shares learning, handles cold start) vs. one model per series (doesn't scale, no cold start). *Why it matters:* the key modern design choice — default to **global** for many related series.
- **ARIMA / ETS / Prophet** — Classical per-series models (autoregressive, exponential smoothing, additive trend/seasonality/holidays). *Why it matters:* strong, interpretable baselines; know when classical beats deep learning (few series, strong seasonality).
- **DeepAR** — A global probabilistic RNN trained across many related series. *Why it matters:* the canonical global deep probabilistic forecaster.
- **Temporal Fusion Transformer (TFT)** — Attention-based multi-horizon model supporting covariates and interpretability. *Why it matters:* the transformer option with covariate handling and some interpretability.
- **Foundation forecasting model** — Pretrained time-series models (TimesFM, Chronos, Moirai, TimeGPT). *Why it matters:* enable zero/few-shot forecasts; the frontier to mention in Extensions.
- **Croston's method** — A technique for intermittent (sparse, zero-heavy) demand. *Why it matters:* the go-to name for lumpy/intermittent series where standard models fail.

### Probabilistic forecasting
- **Probabilistic forecast** — A predicted distribution or quantiles/intervals, not just a point estimate. *Why it matters:* decisions (inventory, staffing) need uncertainty, not a single number.
- **Pinball (quantile) loss** — Loss for evaluating/training quantile forecasts. *Why it matters:* the metric/objective for probabilistic forecasts.
- **Newsvendor** — The cost-optimal stocking quantile equals the underage/overage cost ratio. *Why it matters:* links the forecast **distribution** to the business **decision** — a senior-level connection.

### Metrics & structure
- **MASE / WAPE** — Scaled-vs-naive error / weighted absolute percentage error. *Why it matters:* robust aggregate metrics across many series; preferred over MAPE (which blows up on zeros/low volumes).
- **Seasonal naive** — Baseline predicting the value from the same point in the previous season. *Why it matters:* the bar to beat; if your model can't beat seasonal naive, it's not earning its complexity.
- **Hierarchical forecasting / reconciliation** — Forecasting at multiple aggregation levels and making them coherent (MinT, bottom-up). *Why it matters:* SKU-level and region-level forecasts must add up; reconciliation enforces coherence.

---

*Cross-refs:* feature stores, point-in-time correctness, train/serve skew → Ch. 4/9. Metrics/eval discipline → Ch. 4/8. Batch vs. streaming serving → Ch. 4. Cold start (shared with recsys) → Ch. 9.
