# Engineering Blogs & Papers — Chapter 15 (Forecasting & Prediction)

Curated, interview-relevant reading. Focus on *validation + global modeling + uncertainty*, not chasing SOTA. Search titles if links move.

> **Living note:** forecasting foundation models are new and evolving fast — treat those entries as directional.

## Start here (highest signal)
- **DeepAR** (Salinas et al., Amazon, 2017/2020) — global, probabilistic RNN across related series. The canonical modern forecasting paper.
- **M4 / M5 competition** summaries (Makridakis et al.) — what actually wins at scale (M5 = Walmart demand); global models, gradient boosting, and the value of simple baselines.
- Rob Hyndman's **"Forecasting: Principles and Practice" (FPP)** — the free textbook; backtesting, ETS/ARIMA, hierarchical reconciliation.

## Deep & modern models
- **Temporal Fusion Transformer (TFT)** (Lim et al., Google, 2019) — multi-horizon attention with covariates and interpretability.
- **N-BEATS / N-HiTS** — pure deep-learning forecasting architectures.
- Gradient-boosting for forecasting (LightGBM) — the M5-winning workhorse with engineered lag/calendar features.

## Probabilistic & decisions
- **Pinball / quantile loss** references — evaluating/training quantile forecasts.
- **Newsvendor model** overviews — linking forecast quantiles to inventory decisions.
- Conformal prediction for time series — distribution-free uncertainty (directional).

## Hierarchical & intermittent
- **Hierarchical reconciliation (MinT)** (Wickramasuriya et al.) — coherent multi-level forecasts.
- **Croston's method** and intermittent-demand write-ups — lumpy/sparse series.

## Real-world systems
- **Uber forecasting** posts (Michelangelo, extreme-event forecasting) — demand/marketplace forecasting at scale.
- **Amazon / Meta** demand & capacity forecasting engineering write-ups.

## Foundation forecasting models (frontier)
- **TimesFM** (Google), **Chronos** (Amazon), **Moirai** (Salesforce), **TimeGPT** (Nixtla) — pretrained zero/few-shot time-series models.

## How to use in prep
1. Read the DeepAR paper and an M5 write-up — they anchor global probabilistic modeling and what wins in practice.
2. Be able to explain **rolling-origin backtesting** and **why random splits leak** in one breath.
3. Have **global vs. local** and **WAPE/MASE vs. MAPE** ready.
4. Prepare the **newsvendor** link from forecast quantile to business decision for senior rounds.
