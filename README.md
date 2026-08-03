<div align="center">

# BD Match Pro

### *Where does your asset belong?*
### 你的资产，该卖给谁？

**AI · China Assets · Global Markets**
**AI · 中国资产 · 全球市场**

[![Live demo](https://img.shields.io/badge/🌐_demo-live-d4af37?style=flat-square)](https://sparky-6757.github.io/bd-match-pro/)
[![License: MIT](https://img.shields.io/badge/license-MIT-1a3a5c?style=flat-square)](LICENSE)
[![v1.0.0](https://img.shields.io/github/v/release/sparky-6757/bd-match-pro?style=flat-square&color=0d0c0a)](https://github.com/sparky-6757/bd-match-pro/releases)
[![Stars](https://img.shields.io/github/stars/sparky-6757/bd-match-pro?style=flat-square&color=d4af37)](https://github.com/sparky-6757/bd-match-pro/stargazers)
[![Discussions](https://img.shields.io/github/discussions/sparky-6757/bd-match-pro?style=flat-square&color=1a3a5c)](https://github.com/sparky-6757/bd-match-pro/discussions)

[**🌐 Try the live tool · 立即体验**](https://sparky-6757.github.io/bd-match-pro/) · [**🐙 Source**](https://github.com/sparky-6757/bd-match-pro) · [**🗺️ Roadmap**](https://github.com/sparky-6757/bd-match-pro/issues/2) · [**💬 Discussions**](https://github.com/sparky-6757/bd-match-pro/discussions)

</div>

---

## 🇨🇳 中文

**BD Match Pro** 是一个开源的、AI 驱动的跨境医药授权交易匹配与估值引擎。它针对医药 BD 工作的"第一公里"——*这个品种应该卖给谁？值多少钱？怎么个卖法？*——提供数据化、参数化、可解释的初步答案。

### 它能做什么

1. **匹配买家**——基于 75 家全球战略买家的精选画像（组合策略、地理偏好、近期交易动作），对一个具体品种打分排序，给出**最契合的对手方清单 + 公开联系方式**。
2. **估值与交易结构**——把 **rNPV 风险调整模型** 与 **可比交易回归** 按 50/50 权重融合(可比交易库当前 328 笔，覆盖 2024-11 → 2026-02 公开披露的跨境授权交易；其中 ~50 笔为人工精选含完整临床阶段，其余为批量摄入、临床阶段标记 `unknown`、药物类型按药名规则推断)，给出首付款、里程碑、销售提成的合理区间，并推荐 License-out / NewCo / 联合开发 / 区域分割 等交易结构。当匹配样本 < 3 时模型自动退化为纯 rNPV，并在结果区显式提示。
3. **参数全开放**——成功率（PoS）、贴现率（WACC）、峰值销售、毛利率、爬坡曲线、专利期等核心参数全部可由用户自由调整，**实时**看到不同假设下的估值变化。
4. **方法学透明**——所有公式、参数默认值、买方权重逻辑、相似度加权方式均在源代码与方法学面板中公开，欢迎挑战、修改、改进。

> **关于数据库规模与质量的诚实说明**：v1.0.2 库共 328 笔。其中 53 笔为 v1.0 起就已经手工精选录入的高质量条目（含完整临床阶段、备注），其余 275 笔为从公开披露数据批量摄入——**临床阶段一律标记为 `unknown`，药物类型 (modality) 通过药名规则推断**（如 `-mab` → 单抗、`-tinib` → 小分子、ADC / CAR-T 通过显式 token）。短期路线：(a) 扩充至 500+，(b) 给批量条目回填临床阶段。欢迎在 [Issues](https://github.com/sparky-6757/bd-match-pro/issues) 提交补充数据。

### 为什么开源

医药 BD 长期是少数大行与精英咨询的"黑箱"。本项目想做一件简单的事：**把第一步的方法论开放出来，让中国生物医药资产更高效地走向全球市场**。

> *交易是艺术，不是模型。* 真实成交逻辑与任何预测都可能大相径庭。但只要在 BD 的第一公里，AI 能让大家少走点弯路、提升一点效率，就已经有用了。

---

## 🇬🇧 English

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

## 🚀 Quick start · 快速开始

### Run locally · 本地运行

```bash
git clone https://github.com/sparky-6757/bd-match-pro.git
cd bd-match-pro
# Just open index.html in any modern browser
open index.html              # macOS
xdg-open index.html          # Linux
start index.html             # Windows
```

The entire app is a **single self-contained `index.html` file** — no build step, no backend, no dependencies. All logic lives in plain JavaScript modules within the file.
整个应用是**单一的 `index.html` 文件**——零构建、零后端、零依赖，所有逻辑都用纯 JavaScript 写在文件里。

### Live demo · 在线体验

→ **[https://sparky-6757.github.io/bd-match-pro/](https://sparky-6757.github.io/bd-match-pro/)**

---

## 🧮 Methodology · 方法学

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
**完整方法学在运行中应用的方法学面板里，所有参数都在源码 `index.html` 中可见、可改。**

---

## 🤝 Contributing · 参与贡献

We welcome:
欢迎以下贡献：

- 📊 **Better default parameters** — newer industry data on PoS, WACC, peak sales, ramp curves
  **更准的默认参数**——更新的行业数据（PoS / WACC / 峰值 / 爬坡）
- 💼 **Buyer database updates** — new pipeline portfolios, recent deals, contact corrections
  **买方数据库更新**——新管线组合、近期交易、联系方式修正
- 🧠 **Methodology improvements** — better risk-adjustment math, biosim modelling, NewCo structures
  **方法学改进**——更好的风险调整、生物类似药建模、NewCo 结构
- 🌍 **Indication / TA expansion** — finer subdivisions, regional adjustments
  **适应证 / 治疗领域扩充**——更细分类、地域调整
- 🎨 **Design & UX** — accessibility, mobile, internationalisation
  **设计与体验**——可达性、移动端、国际化
- 🐛 **Bug reports & corrections**
  **Bug 反馈与修正**

### How to contribute · 如何参与

1. **Open an Issue** to discuss the change first (especially for methodology changes).
   先开 Issue 讨论（尤其是方法学改动）。
2. **Fork → branch → PR.** Keep PRs focused; explain *why* in the description.
   Fork → 开分支 → 提 PR；保持改动聚焦，描述里说清**为什么**。
3. **Comment thresholds in the code** if you change a default constant — readers need to know what changed and why.
   修改默认常量请在代码里加注释，让读者知道改了什么、为什么。

---

## 📜 License · 许可

Released under the [MIT License](LICENSE). You may use, modify, distribute, and even commercialise this software freely, provided you retain the copyright notice.
基于 [MIT 协议](LICENSE) 发布。任何人都可以自由使用、修改、分发，甚至商用，只需保留版权声明。

**⚠️ Not investment advice.** Outputs are research-grade estimates. See [DISCLAIMER](DISCLAIMER.md) for the full notice.
**⚠️ 不构成投资建议。** 输出仅为研究级估算，完整免责声明见 [DISCLAIMER](DISCLAIMER.md)。

---

## 💬 Contact · 联系我们 <a id="contact"></a>

- 🌐 Live tool: [sparky-6757.github.io/bd-match-pro](https://sparky-6757.github.io/bd-match-pro/)
- 💡 Feedback and collaboration: **open an [Issue](https://github.com/sparky-6757/bd-match-pro/issues)** or **start a [Discussion](https://github.com/sparky-6757/bd-match-pro/discussions)**

---

<div align="center">

*From China to the World — the first mile, in the open.*
*中国资产 · 全球市场——第一公里，公开可见。*

</div>
