# Contributing to BD Match Pro · 贡献指南

First — thank you. This project gets meaningfully better with every contribution, especially the ones that bring **fresher industry data** or **sharper methodology**.
首先感谢你愿意参与。这个项目每一次有意义的更新，几乎都来自社区——尤其是带来**更新的行业数据**或**更锐利的方法学**的贡献。

---

## Quick rules · 快速准则

1. **Discuss before big changes.** Open an Issue first for methodology / model changes.
   **重要改动先讨论**——方法学 / 模型层面的改动，请先开 Issue。

2. **Keep PRs focused.** One concept per PR. Easier to review, easier to merge.
   **PR 保持聚焦**——一个 PR 解决一件事。

3. **Comment when you change defaults.** If you update `POS`, `WACC`, `RAMP`, `IND_PEAK` etc., add a code comment with: *what changed, source, date*.
   **改默认常量加注释**——改 `POS`、`WACC`、`RAMP`、`IND_PEAK` 等，请注明：**改了什么、来源、日期**。

4. **Keep the file self-contained.** No build step, no npm. The whole app is one `index.html`. If you must add a dependency, make a strong case in the PR description.
   **保持单文件结构**——不引入构建步骤、不加 npm。整个应用就一个 `index.html`。要加依赖请在 PR 描述里充分说明。

5. **Bilingual where it matters.** UI strings should ship in both `<span class="zh-txt">` and `<span class="en-txt">`.
   **关键处保持中英双语**——UI 文案要同时提供 `zh-txt` 与 `en-txt`。

---

## What to contribute · 贡献方向

### 📊 Data updates (highest impact · 影响力最大)

- **`POS` / `BS_POS`** — phase-by-phase probability of success (with citation)
- **`WACC` / `BS_WACC`** — discount rate defaults
- **`IND_PEAK`** — peak-sales benchmarks per indication
- **`RAMP` / `BS_SHARE_RAMP`** — yearly sales ramp curves
- **Buyer database** — portfolio strategy, recent deals, contact info
- **Comparable deals corpus** — add new transactions with structured fields

### 🧮 Methodology

- Better tax/cost-of-goods modelling
- Region-specific NPV adjustments (US / EU / JP / CN)
- Stage-conditional WACC (riskier stage → higher discount)
- Improved biosim share-vs-originator dynamics
- Term-sheet structure-recommendation logic

### 🌍 Coverage

- New indications (esp. rare disease, cell & gene therapy subtypes)
- Modality coverage (RDC, ADC subtypes, mRNA, gene editing, CGT, microbiome…)
- Non-US/EU buyers (JP, KR, IN, MENA, LATAM)

### 🎨 UX

- Accessibility (WCAG AA)
- Mobile-friendly interactions
- Print/PDF export of full valuation report
- Save/load asset profiles via URL hash

### 🐛 Bugs & corrections

- Open an Issue with: steps to reproduce, expected vs. actual, browser
- For data corrections, please cite the source

---

## Workflow · 工作流

```bash
# 1. Fork on GitHub, then clone your fork
git clone https://github.com/<your-username>/bd-match-pro.git
cd bd-match-pro

# 2. Create a focused branch
git checkout -b fix/buyer-pfizer-recent-deals

# 3. Edit index.html — open it in a browser to test as you go
open index.html

# 4. Commit with a clear message
git commit -m "Update Pfizer recent deals (Q1 2026 acquisitions)"

# 5. Push and open a PR
git push origin fix/buyer-pfizer-recent-deals
```

In the PR description, include:
PR 描述请包含：

- **What changed** (1–2 sentences)
- **Why** (the data source, the methodology rationale, the UX rationale)
- **Sources** (links to public deal disclosures, papers, regulatory filings, etc.)
- **Screenshot** if it's a UI change

---

## Reviews & merging · 审核与合并

- Project maintainers will review within ~3–5 business days.
- Methodology PRs may take longer if they require reproducing the math.
- Once merged, your contribution ships to https://sparky-6757.github.io/bd-match-pro/ within ~2 minutes.

---

## Code of conduct · 行为准则

Be kind. Disagree on substance, not on people. This is a tool for the global biopharma BD community — keep it welcoming for newcomers.
请保持友善。可以在内容上争论，不要做人身攻击。这是为全球生物医药 BD 社区做的工具——请让新来者感到欢迎。

---

## Questions? · 有问题？

- 💬 [GitHub Discussions](https://github.com/sparky-6757/bd-match-pro/discussions) — for open-ended questions
- 🐛 [Issues](https://github.com/sparky-6757/bd-match-pro/issues) — for specific bugs or proposals
- 📧 Direct contact: see [README · Contact](README.md#contact)
