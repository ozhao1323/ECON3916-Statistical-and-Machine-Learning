# Audit 02: Deconstructing Statistical Lies

**Role:** Data Quality Auditor | **Firm:** Pareto Ventures (Series B VC)  
**Module:** Probability, Robustness & Sampling | **Course:** ECON 3916  

---

## Overview

Three portfolio companies each claimed "perfect" metrics. This audit uses forensic statistics to find the lie hidden inside their averages — demonstrating why summary statistics without distributional context are not just incomplete, but actively misleading.

---

## Finding 1 — Latency Skew: The Vanity Metric Trap

**Company:** NebulaCloud | **Claim:** "Mean latency of 35ms"  
**Verdict:** ⚠️ Technically true. Forensically useless.

NebulaCloud's mean latency of 35ms is mathematically correct — and completely deceptive. Simulating their Data Generating Process (1,000 requests: 980 normal at 20–50ms, 20 spike events at 1,000–5,000ms) reveals the danger of Standard Deviation as a robustness metric.

| Metric | Value |
|---|---|
| Standard Deviation | ~312 ms |
| Median Absolute Deviation (MAD) | ~7 ms |

SD squares every deviation, so the 20 outlier spikes — just 2% of traffic — each contribute ~9,000,000 to the sum, completely dominating the result. MAD takes the median of absolute deviations, so those same 20 spikes get outvoted by the 980 normal requests. The MAD of 7ms accurately reflects what 98% of users experience. The SD of 312ms reveals a serious P99 tail latency problem that will breach SLAs and drive churn.

**Key Takeaway:** Always audit tail latency, not mean latency. A system can have a "great" mean and a catastrophic P99.

---

## Finding 2 — The False Positive Paradox: Base Rate Neglect

**Company:** IntegrityAI | **Claim:** "98% accurate plagiarism detector (Sensitivity = Specificity = 98%)"  
**Verdict:** ❌ Dangerous in low-prevalence contexts.

Using Bayes' Theorem to calculate P(Actually Cheating | Flagged) across three deployment contexts:

```
P(Cheater | Flagged) = [P(Flagged | Cheater) × P(Cheater)] / P(Flagged)
```

| Scenario | Base Rate | P(Actually Cheating \| Flagged) |
|---|---|---|
| A — Bootcamp | 50.0% | **98.00%** — tool works as advertised |
| B — Econ Class | 5.0% | **72.06%** — 1 in 4 flags is a false accusation |
| C — Honors Seminar | 0.1% | **4.68%** — 19 in 20 flags are innocent students |

IntegrityAI's "98% accuracy" is only meaningful when cheating is common. In the Honors Seminar context, the pool of innocent students is so large that the 2% false positive rate generates far more false flags than true ones. Deploying this tool in low-prevalence environments would result in systematic false accusations — a textbook case of **base rate neglect**.

**Key Takeaway:** Sensitivity and specificity scores are meaningless without knowing the base rate of the population being tested. Always compute posterior probability before deploying a classifier.

---

## Finding 3 — Survivorship Bias: The Graveyard Nobody Shows You

**Company:** FinFlash (Crypto) | **Claim:** "Strong portfolio returns across token launches"  
**Verdict:** ❌ 211× inflation from survivorship bias.

Simulating 10,000 token launches using a Pareto distribution (power law, shape = 0.8) to model realistic crypto market dynamics — where 99% of tokens go near-zero and a handful capture all the value.

| Dataset | n | Mean Peak Market Cap |
|---|---|---|
| `df_all` — The Graveyard (all tokens) | 10,000 | ~$421,836 |
| `df_survivors` — Top 1% only | 100 | ~$89,204,711 |
| **Survivorship Bias Multiplier** | | **~211×** |

Every fund manager showing "average portfolio returns" on crypto is implicitly showing `df_survivors` while calling it `df_all`. Filtering to the top 1% by peak market cap shifts the mean by over 200×. The dual histogram makes this visceral: the full distribution is a near-vertical wall at the low end with an extreme right tail, while the survivors-only view looks like a healthy, high-performing asset class.

**Key Takeaway:** Always ask which tokens, funds, or strategies are missing from the sample. The graveyard is the data.

---

## Methods & Stack

```python
numpy        # DGP simulation, Pareto distribution, vector operations
pandas       # DataFrame construction and filtering
matplotlib   # Dual histogram visualization
# All core functions (MAD, Bayes, Chi-Square) written from scratch — no scipy
```

**Statistical techniques:** Median Absolute Deviation (MAD), Bayes' Theorem, Chi-Square Goodness of Fit, Pareto/Power Law simulation, Sample Ratio Mismatch (SRM) detection.

---

## Broader Lesson

Each company told a true fact. NebulaCloud's mean really was 35ms. IntegrityAI's detector really is 98% accurate. FinFlash's survivors really did generate those returns. The lie was not in the numbers — it was in the choice of which statistic to report and which population to measure. Forensic auditing is the practice of asking: *what is this average hiding?*

---

*Part of the ECON 3916 Algorithmic Audit series — applying probability and statistical robustness to VC due diligence.*
