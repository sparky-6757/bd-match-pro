<div align="center">


<div align="center">
# BD Match Pro

**BD Match Pro** is an open-source, AI-powered cross-border licensing engine for pharmaceutical assets. It tackles the first mile of biotech business development — *who would buy this asset, at what price, and via which deal structure?* — with data-driven, fully parametric, and transparent first-pass answers.

### What it does

1. **Match buyers** — score and rank 75 deeply profiled global strategic acquirers against your asset, based on portfolio fit, geographic preference and recent deal activity. Output includes **buyer profile, financial snapshot, recent transactions and public contact details**.
2. **Value & structure** — blend **risk-adjusted NPV** with a **comparable-deal regression** at 50/50 weight (the comp database currently holds 328 publicly disclosed cross-border deals from 2024-11 → 2026-02; ~50 are hand-curated with full clinical-stage detail, the remainder are bulk-ingested with **clinical stage marked `unknown`** and **modality inferred from drug-name patterns**); size upfront / milestones / royalty ranges; recommend License-out, NewCo, Co-development or Regional split structures. When fewer than 3 similar comps exist, the model falls back to pure rNPV — transparently flagged in the result panel.
3. **Fully parametric** — every input (PoS, WACC, peak sales, margin, ramp curve, patent runway, etc.) is **user-adjustable** and the valuation re-renders in real time.
4. **Transparent methodology** — every formula, default parameter, weight and similarity-scoring rule is documented in the methodology panel and in the source. Challenge it, fork it, improve it.

> **An honest note about database size and quality**: the v1.0.2 database is 328 deals total — 53 hand-curated entries from v1.0 (full clinical-stage detail and editorial notes), plus 275 bulk-ingested from public deal data with **clinical stage marked `unknown`** and **modality inferred from drug-name patterns** (e.g. `-mab` → mAb, `-tinib` → small molecule, ADC / CAR-T from explicit tokens). Near-term priorities: (a) expand to 500+, (b) backfill clinical stage on the bulk-ingested entries. Submit additional public deals via [Issues](https://github.com/sparky-6757/bd-match-pro/issues).

### Why open-source

Pharma BD has long been the black box of a handful of bulge-bracket banks and elite consultancies. This project does one simple thing: **open up the first-pass methodology so that Chinese biopharma assets can find their way to global markets more efficiently.**

> *Deals are art, not models.* Real-world outcomes diverge from any forecast. But if AI can save practitioners a few wrong turns at the very first mile, it has already earned its keep.

---

## 🚀 Quick start
### Run locally
```bash
git clone https://github.com/sparky-6757/bd-match-pro.git
cd bd-match-pro
# Just open index.html in any modern browser
open index.html              # macOS
xdg-open index.html          # Linux
start index.html             # Windows
```

The entire app is a **single self-contained `index.html` file** — no build step, no backend, no dependencies. All logic lives in plain JavaScript modules within the file.
** `index.html` **——、、， JavaScript 。

### Live demo
→ **[https://sparky-6757.github.io/bd-match-pro/](https://sparky-6757.github.io/bd-match-pro/)**

---

## 🧮 Methodology
The valuation engine runs two independent paths and blends them at 50/50 (when ≥ 3 similar comps exist):

### 1 · Parametric path — Risk-adjusted NPV (rNPV)

```
rNPV_licensor = PoS × Σ_t  [ Peak × Ramp(t) × ModPremium × CompMult × RoyaltyRate ] / (1 + WACC)^t
rNPV_asset    = PoS × Σ_t  [ Peak × Ramp(t) × ModPremium × CompMult × NetMargin ]   / (1 + WACC)^t
```

- **PoS_cumulative** — Preclinical 5% → Phase I 10% → Phase II 17% → Phase III 52% → NDA 88% → Approved 100% (BIO/QLS/Informa benchmarks, user-editable)
- **WACC** — default 11% (user-adjustable)
- **Patent runway** — 10 years post-approval; ramp curve 10/30/60/85/100/100/95/80/55/25
- **ModPremium** — sm 1.00 · mab 1.05 · bsab 1.25 · adc 1.40 · cart 1.50 · gt 1.55 · pep 1.10 · olig 1.20 · rc 1.45

### 2 · Data path — Comparable-deal regression

For each deal in `DEALS_DB` (currently 328 cross-border licensing deals with disclosed economics — 53 hand-curated with full detail, 275 bulk-ingested with `stage:unknown` and inferred modality), compute a similarity weight:

```
weight(d) = 0.02 (baseline)
          + 0.50 (indication direct hit) | 0.25 (adjacent) | 0.10 (same TA)
          + 0.30 (modality direct hit)   | 0.08 × ratio(ModPremium) (mismatch)
          + 0.20 (stage hit) | 0.10 (±1 stage) | 0.04 (±2 stages)
```

Deals passing a real-similarity gate (indication ≥ adjacent OR modality direct match OR weak triple of indication/modality/stage) are weighted-resampled, then quantiles taken:

```
total_implied   = median(samples) × stage_correction × mod_correction × terr_factor
upfront_implied = median(samples.upfront)         × (same correction terms)
P10 / P90       = 20% / 80% quantiles of resampled distribution
```

### 3 · Blended output

```
total_blended    = 0.5 × rNPV_total   + 0.5 × total_implied      // when N ≥ 3
upfront_blended  = 0.5 × rNPV_upfront + 0.5 × upfront_implied
P10 / P90        = union(rNPV sensitivity, comp quantile)        // conservative
```

When fewer than 3 similar comps exist, the model falls back to pure rNPV and the result panel explicitly says so.

### 4 · Biosimilar valuation

A separate model with biosim-specific PoS (higher), WACC (lower, 9%), gross margin (~55%), share-of-originator ramp curve, and discount-vs-originator parameter. **Biosim does not currently use comp-blending** — DEALS_DB carries too few biosim transactions to support the regression.

### 5 · Buyer matching

```
Score = 40·IndicationFit + 25·ModalityFit + 20·StageFit + 10·FinancialCapacity + 5·RecentActivity
```

Each axis is documented in the methodology panel with its sub-weights.

### Known limitations

- **Modest sample** — 328 disclosed-economics deals; statistical confidence improves with sample size but P10/P90 bands still run wide for narrow indication × stage × modality slices.
- **Inferred fields on 275 of 328 entries** — clinical stage is `unknown` and modality is inferred from drug-name patterns; an entry with `ind:unknown` contributes only via modality match in the similarity-weighted regression and is appropriately downweighted in the median, but it does inflate the displayed `N`.
- **Selection bias** — database over-indexes China license-outs vs. pure overseas in-licensing.
- **Biobucks inflation** — reported "total deal value" often inflates distant sales milestones.
- **No biosim regression** — too few biosim deals to support a separate regression.

**Full methodology panel is in the running app (Methodology tab); all parameters are visible & editable in the source `index.html`.**
**， `index.html` 、。**

---

## 🤝 Contributing
We welcome:
：

- 📊 **Better default parameters** — newer industry data on PoS, WACC, peak sales, ramp curves
  ****——（PoS / WACC /  / ）
- 💼 **Buyer database updates** — new pipeline portfolios, recent deals, contact corrections
  ****——、、
- 🧠 **Methodology improvements** — better risk-adjustment math, biosim modelling, NewCo structures
  ****——、、NewCo
- 🌍 **Indication / TA expansion** — finer subdivisions, regional adjustments
  ** / **——、
- 🎨 **Design & UX** — accessibility, mobile, internationalisation
  ****——、、
- 🐛 **Bug reports & corrections**
  **Bug **

### How to contribute
1. **Open an Issue** to discuss the change first (especially for methodology changes).
    Issue （）。
2. **Fork → branch → PR.** Keep PRs focused; explain *why* in the description.
   Fork →  →  PR；，****。
3. **Comment thresholds in the code** if you change a default constant — readers need to know what changed and why.
   ，、。

---

## 📜 License
Released under the [MIT License](LICENSE). You may use, modify, distribute, and even commercialise this software freely, provided you retain the copyright notice.
 [MIT ](LICENSE) 。、、，，。

**⚠️ Not investment advice.** Outputs are research-grade estimates. See [DISCLAIMER](DISCLAIMER.md) for the full notice.
**⚠️ 。** ， [DISCLAIMER](DISCLAIMER.md)。

---

## 💬 Contact ·  <a id="contact"></a>

- 🌐 Live tool: [sparky-6757.github.io/bd-match-pro](https://sparky-6757.github.io/bd-match-pro/)
- 💡 Feedback and collaboration: **open an [Issue](https://github.com/sparky-6757/bd-match-pro/issues)** or **start a [Discussion](https://github.com/sparky-6757/bd-match-pro/discussions)**

---

<div align="center">
