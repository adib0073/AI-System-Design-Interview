# Common Interviewee Doubts — Chapter 15 (Forecasting & Prediction)

The questions candidates most often have about forecasting rounds. Grouped by theme.

---

## Leakage & validation (do this right or fail)

**1. What's the most common forecasting mistake?**
**Temporal leakage.** Using a random train/test split (which mixes future into training), or features computed with future information. Always split by **time** and use only **point-in-time** features (what was known at prediction time). Say this early — it's the fastest credibility signal.

**2. How do I validate a forecasting model?**
**Rolling-origin (walk-forward) backtesting:** train on data up to time t, predict the next horizon, roll t forward, repeat. This mimics production and gives honest error across many origins. Never k-fold cross-validate a time series.

**3. How do I build features without leaking?**
Lags, rolling stats (mean/std over past windows), and calendar features (day-of-week, holidays, seasonality) — all computed **only from the past** relative to each prediction point. Watch rolling windows that accidentally include the target period.

## Model choice

**4. Global model or one model per series?**
Default to a **global** model trained across all series when you have many related ones (products, stores). It scales, shares learning across series, and handles **cold start** (a new SKU borrows patterns). One-model-per-series doesn't scale to millions and can't forecast new series. This is the key modern design choice.

**5. Classical (ARIMA/Prophet) or deep learning?**
Classical models are strong, interpretable baselines — often best for **few series with clear seasonality**. Deep global models (DeepAR/TFT) win with **many related series** and rich covariates. Always start from a **seasonal-naive baseline** and justify complexity by beating it.

**6. When do I mention foundation forecasting models?**
In Extensions. Pretrained time-series models (TimesFM, Chronos, Moirai, TimeGPT) offer zero/few-shot forecasts — useful for cold start or many-series settings. Mention with the caveat that they're newer and need validation on your data.

## Point vs. probabilistic

**7. Point forecast or distribution?**
Prefer **probabilistic** (quantiles/intervals) because downstream decisions need uncertainty. Inventory, staffing, and capacity planning use quantiles, not a single number. Train/evaluate with **pinball (quantile) loss**.

**8. How does the forecast connect to the business decision?**
Via the **newsvendor** logic: the optimal stocking quantile equals the ratio of underage to (underage + overage) cost. So a costly stockout → forecast a higher quantile. Connecting the forecast distribution to the decision is a senior-level move.

## Metrics

**9. Why not MAPE?**
MAPE blows up (or is undefined) on zeros and low volumes — common in demand data. Use **WAPE** (weighted absolute percentage error) and **MASE** (scaled against a naive baseline), which are robust across many series of different scales.

**10. My forecasts at SKU and region level don't add up — what do I do?**
**Hierarchical reconciliation** (bottom-up, MinT) makes multi-level forecasts coherent so they sum correctly. Mention it when the prompt has natural hierarchies (SKU → category → region → total).

## Edge cases & delivery

**11. How do I handle intermittent/lumpy demand?**
Many zeros with occasional spikes break standard models. Use **Croston's method** or intermittent-demand-specific approaches, and prefer distributional metrics.

**12. How do I handle a brand-new product (cold start)?**
A **global** model helps immediately (borrow from similar products); use attributes/covariates, analog products, and hierarchy. This is the same exploration/cold-start theme as recsys.

**13. How do I structure the answer under time pressure?**
Clarify (what/horizon/granularity, how the forecast is used) → features (point-in-time, no leakage) → model (seasonal-naive baseline → global DeepAR/TFT, classical where apt) → **probabilistic** output tied to the decision (newsvendor) → **rolling-origin backtesting** + WAPE/MASE → cold start/intermittent/hierarchy → serving (usually batch). Lead with leakage + global model.
