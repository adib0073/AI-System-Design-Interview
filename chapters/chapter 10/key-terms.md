# Key Terms — Chapter 10 (Ads Ranking & Computational Advertising)

Interview-oriented definitions for the vocabulary in Chapter 10 (scanned from the chapter glossary and prose). Each pairs a crisp definition with *why it matters*. Feeds the cumulative book glossary.

---

### Auctions & mechanisms
- **GSP (Generalized Second-Price)** — Multi-slot auction ranking by score; each winner pays roughly the next competitor's price. *Why it matters:* the historical workhorse; simple but **not strictly truthful**, so advertisers game bids.
- **Second-price / Vickrey** — Winner pays the next-highest bid. *Why it matters:* makes truthful bidding a dominant strategy (single slot); the conceptual baseline.
- **VCG (Vickrey-Clarke-Groves)** — Truthful multi-slot mechanism where each winner pays the externality it imposes on others. *Why it matters:* theoretically clean (Meta/Facebook uses VCG-style); harder to explain to advertisers.
- **RTB (Real-time bidding)** — Programmatic per-impression auctions on external exchanges within ~100 ms; typically first-price today. *Why it matters:* the open-web ads path; latency and first-price bidding change the design.
- **Bid shading** — Reducing a bid below true value in a first-price auction to avoid overpaying. *Why it matters:* the first-price analog of truthful bidding; a platform service in RTB.
- **Reserve price** — Minimum eCPM required to win a slot. *Why it matters:* trades revenue floor against fill rate.

### Ranking value & prediction
- **eCPM (expected cost per mille)** — Expected revenue per 1,000 impressions; pCTR × bid × 1000 (CPC) or pCTR × pCVR × bid × 1000 (CPA). *Why it matters:* **the ranking score** — ads rank by expected revenue, not raw relevance.
- **CTR / CVR** — p(click | impression) / p(conversion | click). *Why it matters:* the two predictions that feed eCPM.
- **pCTR / pCVR** — Predicted CTR / CVR. *Why it matters:* the models you build; their **calibration** (not just ranking) is critical.
- **Calibration** — Predicted probabilities match observed frequencies. *Why it matters:* the ads-specific must-mention — because eCPM *multiplies* pCTR/pCVR by bids, miscalibration directly distorts price and revenue (unlike organic ranking, where only order matters).
- **ESMM (Entire Space Multi-Task Model)** — Trains pCTR and pCTCVR over all impressions and derives pCVR = pCTCVR / pCTR. *Why it matters:* avoids the **click-only selection bias** that plagues naïve pCVR models (conversions are only observed after clicks).
- **Wide & Deep** — Linear (memorization) + deep (generalization) components. *Why it matters:* influential CTR architecture; good lineage to cite.

### Bidding, budgets & quality
- **Auto-bidding (value-based bidding)** — Platform sets per-auction bids from an advertiser goal (target CPA/ROAS or max-conversions). *Why it matters:* modern advertisers set goals, not bids; the platform optimizes on their behalf.
- **CPC / CPM / CPA** — Pricing by click / per 1,000 impressions / per conversion. *Why it matters:* the billing models that determine the eCPM formula used.
- **Budget pacing** — Controller spreading a campaign's spend across its period via throttling or bid modulation. *Why it matters:* prevents blowing the budget by noon; a control-systems problem interviewers probe.
- **Frequency capping** — Limiting how often a user sees a given ad/advertiser. *Why it matters:* reduces fatigue and protects long-term user value.
- **Ad Rank** — Ranking value combining bid, predicted CTR, and ad quality/relevance. *Why it matters:* quality is a first-class ranking factor — bad ads don't win just by bidding high.
- **Attribution window** — Period after a click during which a conversion is credited (1-, 7-, 28-day). *Why it matters:* defines labels and creates **delayed feedback** — conversions arrive after the ad served.

### Pipeline & privacy
- **Pre-ranking** — Lightweight scoring stage between retrieval and full ranking. *Why it matters:* the ads funnel (like recsys) needs a cheap cut before heavy ranking under tight latency.
- **Delayed feedback** — Conversions arrive hours/days after the click. *Why it matters:* you must train pCVR with incomplete labels (delayed-feedback models, importance weighting).
- **Privacy-preserving ads (ATT, Privacy Sandbox)** — Apple App Tracking Transparency, Google's Privacy Sandbox (Topics, aggregated attribution). *Why it matters:* signal loss reshapes targeting/attribution; a mandatory modern topic — mention on-device and aggregated measurement.

---

*Cross-refs:* the multi-stage funnel, two-tower retrieval, DLRM ranking → Ch. 9. Latency budgets/serving → Ch. 3/9. A/B and guardrail metrics → Ch. 8. Bias/selection bias → Ch. 12 (reject inference is the analog).
