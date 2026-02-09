# Lab 5: The Architecture of Bias

## Overview
This project systematically investigates how data collection and sampling methodologies introduce structural biases in machine learning pipelines. Through empirical simulation and statistical testing, I analyzed the Data Generating Process (DGP) to identify and mitigate common sources of bias that compromise model validity.

## Technical Implementation

**Tech Stack:** Python, pandas, numpy, scipy, scikit-learn

### 1. Simple Random Sampling Analysis
Manually simulated random sampling on the Titanic dataset to quantify sampling error and variance. Demonstrated that uncontrolled random sampling produces unstable class distributions across draws, particularly for minority classes, leading to inconsistent model training conditions.

### 2. Stratified Sampling for Covariate Shift Elimination
Implemented stratified sampling using `sklearn.model_selection.StratifiedShuffleSplit` to preserve population-level class distributions in training/test splits. This approach eliminates covariate shift by ensuring representative samples across survival classes, reducing variance and improving generalization estimates.

### 3. Sample Ratio Mismatch (SRM) Forensic Audit
Conducted chi-square goodness-of-fit tests to detect Sample Ratio Mismatch in A/B test scenarios. Validated that observed assignment ratios deviating significantly from expected distributions (p < 0.01) indicate systematic engineering failures (e.g., biased load balancers, faulty randomization) rather than natural variance.

**Key Result:** A 550/450 split in a planned 50/50 experiment represents a 3.16σ deviation—occurring by chance only ~0.16% of the time, providing strong evidence of infrastructure failure.

## Theoretical Deep Dive: Survivorship Bias in Startup Analysis

### The Problem
Analyzing only successful unicorn startups featured on TechCrunch creates **survivorship bias**—a form of selection bias where the sample is conditioned on a post-outcome variable (success). This systematically excludes failed startups from the dataset, distorting causal inference about what drives startup success.

**Why it matters:** Patterns observed in survivors (e.g., "pivoted early," "raised seed funding quickly") may actually be equally common among failures. Without the counterfactual data, we can't distinguish genuine success factors from spurious correlations.

### The Ghost Data
To correct survivorship bias using a **Heckman Correction** (two-stage selection model), I would need:

1. **Selection-stage data (Stage 1):** Features predicting *whether a startup gets observed* (i.e., reaches media coverage or survival threshold)
   - Founder network strength (LinkedIn connections, prior startup experience)
   - Initial funding amount and investor prestige
   - Geographic location (proximity to tech hubs)
   - Industry sector and founding year

2. **Outcome-stage data (Stage 2):** Features predicting *unicorn status among survivors*
   - Revenue growth rates
   - Product-market fit metrics
   - Time-to-market velocity

**Critical Ghost Data:** Information on **failed startups** that never reached TechCrunch visibility—including their founding characteristics, initial traction metrics, and failure timing. This is typically inaccessible but could be approximated through:
- Crunchbase entries for defunct companies
- AngelList profiles of shuttered ventures  
- VC portfolio companies with unreported outcomes

### The Heckman Mechanism
The correction estimates a **selection equation** modeling P(observed | X) and incorporates the inverse Mills ratio (λ) into the outcome regression. This adjusts for correlation between unobserved factors affecting both selection (media coverage) and outcome (unicorn status), recovering unbiased estimates of success determinants.

**Bottom line:** Without the "graveyard" of failed startups, any analysis is fundamentally analyzing *what makes survivors different from each other*—not what makes companies succeed vs. fail.

---

## Key Takeaway
Bias in machine learning isn't just about algorithmic fairness—it's encoded in the data collection process itself. Understanding the DGP and applying appropriate sampling strategies is essential for building models that generalize beyond the observed sample.
