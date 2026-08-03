# Contributing to BD Match Pro
First — thank you. This project gets meaningfully better with every contribution, especially the ones that bring **fresher industry data** or **sharper methodology**.
。，——********。

---

## Quick rules
1. **Discuss before big changes.** Open an Issue first for methodology / model changes.
   ****—— / ， Issue。

2. **Keep PRs focused.** One concept per PR. Easier to review, easier to merge.
   **PR **—— PR 。

3. **Comment when you change defaults.** If you update `POS`, `WACC`, `RAMP`, `IND_PEAK` etc., add a code comment with: *what changed, source, date*.
   ****—— `POS`、`WACC`、`RAMP`、`IND_PEAK` ，：**、、**。

4. **Keep the file self-contained.** No build step, no npm. The whole app is one `index.html`. If you must add a dependency, make a strong case in the PR description.
   ****——、 npm。 `index.html`。 PR 。

5. **Bilingual where it matters.** UI strings should ship in both `<span class="zh-txt">` and `<span class="en-txt">`.
   ****——UI  `zh-txt`  `en-txt`。

---

## What to contribute
### 📊 Data updates (highest impact · )

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

## Workflow
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
PR ：

- **What changed** (1–2 sentences)
- **Why** (the data source, the methodology rationale, the UX rationale)
- **Sources** (links to public deal disclosures, papers, regulatory filings, etc.)
- **Screenshot** if it's a UI change

---

## Reviews & merging
- Project maintainers will review within ~3–5 business days.
- Methodology PRs may take longer if they require reproducing the math.
- Once merged, your contribution ships to https://sparky-6757.github.io/bd-match-pro/ within ~2 minutes.

---

## Code of conduct
Be kind. Disagree on substance, not on people. This is a tool for the global biopharma BD community — keep it welcoming for newcomers.
。，。 BD ——。

---

## Questions? · ？

- 💬 [GitHub Discussions](https://github.com/sparky-6757/bd-match-pro/discussions) — for open-ended questions
- 🐛 [Issues](https://github.com/sparky-6757/bd-match-pro/issues) — for specific bugs or proposals
- 📧 Direct contact: see [README · Contact](README.md#contact)
