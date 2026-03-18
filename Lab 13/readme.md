# The Architecture of Dimensionality: Hedonic Pricing & the FWL Theorem

## Objective
Executed a multivariate hedonic pricing model on 2026 California real estate data to empirically validate the Frisch-Waugh-Lovell theorem, demonstrating that algorithmic dimensionality control produces exact coefficient equivalence to full multivariate OLS estimation.

## Methodology
- **Hedonic OLS Specification** — Regressed `Sale_Price` on `Property_Age` and `Distance_to_Tech_Hub` using `statsmodels.formula.api`, constructing a multivariate pricing model that treats real estate value as a function of decomposable structural attributes.
- **Omitted Variable Bias Isolation** — Estimated a bivariate model omitting `Distance_to_Tech_Hub` to empirically quantify the OVB magnitude, surfacing the extent to which uncontrolled spatial proximity contaminates the age coefficient.
- **FWL Residual Partialling** — Manually implemented the Frisch-Waugh-Lovell theorem by (1) regressing `Sale_Price` on `Distance_to_Tech_Hub` and extracting residuals, (2) regressing `Property_Age` on `Distance_to_Tech_Hub` and extracting residuals, then (3) regressing the first residual vector on the second — fully purging the shared covariance structure between predictors.
- **Coefficient Verification** — Confirmed exact numerical equivalence between the FWL-derived partial coefficient on `Property_Age` and the multivariate OLS estimate, proving algebraic ceteris paribus at machine precision.

## Key Findings
Omitting `Distance_to_Tech_Hub` from the pricing model produced severe omitted variable bias: the bivariate coefficient on `Property_Age` was materially inflated, falsely attributing pricing power to physical home age that properly belonged to spatial proximity to the tech hub. Because `Property_Age` and `Distance_to_Tech_Hub` share negative covariance in the California market — newer developments cluster near tech corridors — their explanatory overlap contaminated the naive estimate.

Manual execution of the FWL theorem successfully decomposed this shared variance. By partialling out `Distance_to_Tech_Hub` from both the outcome and the focal predictor before re-estimating, the residual regression recovered the true partial effect of `Property_Age` — an exact match to the full multivariate coefficient. This constitutes a ground-up proof that OLS dimensionality control is not a statistical approximation but a precise algebraic operation: the multivariate estimator mechanically performs the same orthogonalization that FWL executes explicitly.

---

**Tech Stack:** Python 3.10+ · pandas · statsmodels.formula.api · matplotlib · Zillow Synthetic Data (California, 2026)
