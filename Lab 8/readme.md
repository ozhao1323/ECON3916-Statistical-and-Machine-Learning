# Hypothesis Testing & Causal Evidence Architecture

## Objective
This project operationalizes the scientific method to adjudicate between competing narratives of causality using the Lalonde (1986) dataset. The core pivot: rather than simply *estimating* treatment effects, the analysis is framed around *falsification* — asking not "what is the effect?" but "could this result be noise?"

## Technical Approach
- Computed the Average Treatment Effect (ATE) via Welch's T-Test, treating the T-statistic as a **Signal-to-Noise ratio** to measure effect magnitude against sampling variance
- Validated parametric results with a **Non-Parametric Permutation Test** (10,000 resamples), stress-testing assumptions against non-normal earnings distributions
- Controlled for Type I error risk using α = 0.05 as the decision threshold, with cross-validation between both testing frameworks

## Key Findings
Detected a statistically significant lift in real earnings of ~$1,795 (p < 0.05), rejecting the Null Hypothesis via Proof by Statistical Contradiction. Permutation and parametric p-values converged, confirming result robustness.

## Business Insight
Rigorous hypothesis testing is the **safety valve of the algorithmic economy**. In production environments — recommendation engines, pricing models, platform experiments — unchecked correlations masquerade as causation at scale. Formalizing falsification pipelines prevents data grubbing and protects decision-making from spurious signals before they compound downstream.
