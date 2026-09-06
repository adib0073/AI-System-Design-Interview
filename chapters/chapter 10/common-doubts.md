# Common Interviewee Doubts — Chapter 10 (Ads Ranking & Computational Advertising)

The questions candidates most often have about ads-ranking rounds. Grouped by theme.

---

## Ads vs. organic recommendations

**1. How is ads ranking different from the Chapter 9 feed?**
It reuses the funnel, but adds three things: (1) an **auction** decides who wins and what they pay, (2) it ranks by **eCPM** (expected revenue), not pure relevance, and (3) **calibration** of predicted probabilities is critical because they set prices. Lead with these deltas — don't re-derive the whole funnel.

**2. What do ads rank by?**
**eCPM** = expected revenue per 1,000 impressions. For CPC: pCTR × bid. For CPA: pCTR × pCVR × bid. Plus an ad-quality/relevance term (Ad Rank) so high-bidding bad ads don't win. It balances **advertiser value, platform revenue, and user experience** simultaneously.

## Calibration (the signature topic)

**3. Why does calibration matter here when it didn't in organic ranking?**
In organic ranking only the **order** matters, so an uncalibrated score is fine. In ads, the predicted probability is **multiplied by a bid to compute price and rank**. If pCTR is 2× too high, eCPM and the charged price are wrong — you mis-rank and mis-bill. So ads models must be **calibrated**, not just good at ordering. This is the #1 ads-specific insight.

**4. How do I calibrate?**
Post-hoc methods (Platt scaling, isotonic regression), calibration-aware training, and monitoring calibration curves in production. Recalibrate as distributions drift.

## Prediction challenges

**5. Conversions happen days after the click — how do I train pCVR?**
This is **delayed feedback**. At training time many recent conversions haven't arrived yet, so labels are incomplete. Use delayed-feedback models (model the delay distribution), importance weighting, or wait-and-attribute windows. Acknowledge the bias explicitly.

**6. pCVR is only observable after a click — isn't that biased?**
Yes — **click-only selection bias**. Training pCVR only on clicked impressions distorts it. **ESMM** solves this by modeling pCTR and pCTCVR over the *entire* impression space and deriving pCVR = pCTCVR / pCTR. Naming ESMM here is a strong signal.

## Auctions

**7. Do I need auction theory?**
Know the intuition, not proofs. **Second-price/Vickrey** → truthful bidding is optimal (single slot). **GSP** → the multi-slot generalization Google used; simple but not strictly truthful. **VCG** → truthful multi-slot (pay your externality), used by Meta. **RTB** on exchanges is usually **first-price** today, so platforms do **bid shading**. Be able to say why truthfulness is desirable (advertisers can bid true value).

**8. First-price or second-price — which and why?**
Historically second-price/GSP for owned surfaces (truthful, simpler for advertisers). Open exchanges moved to **first-price** (transparency), which pushes bid-shading services. Mention reserve prices as the revenue floor.

## Budgets, quality & privacy

**9. What is budget pacing and why is it hard?**
Spreading a campaign's budget smoothly over its window (a day/month) instead of exhausting it early. It's a **control problem** — throttle participation or modulate bids based on spend-so-far vs. target. Interviewers like a feedback-controller framing.

**10. How do I keep ad quality up?**
Quality/relevance is a ranking factor (Ad Rank), plus landing-page quality, policy/safety filters, and frequency capping to limit fatigue. A pure revenue-max objective destroys long-term user value — say so.

**11. How do I handle the privacy shift (ATT / Privacy Sandbox)?**
Signal loss from Apple's ATT and third-party-cookie deprecation reduces user-level tracking. Move toward **aggregated/on-device measurement** (Privacy Sandbox: Topics, Attribution Reporting), modeled conversions, and first-party data. This is a mandatory modern topic for senior rounds.

## Delivery

**12. How do I structure the answer under time pressure?**
Clarify (surface, CPC/CPA, objective) → funnel (retrieval → pre-rank → rank by eCPM) → prediction (pCTR/pCVR, **calibration**, ESMM/delayed feedback) → auction (GSP/VCG, pricing) → bidding & **pacing** → quality/frequency → **privacy** → evaluation (revenue + user guardrails via A/B). The eCPM + calibration + auction core is what's graded.
