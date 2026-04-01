## AI Capex Diagnostic Modeling
`Python` `pandas` `statsmodels` `matplotlib` `seaborn`

**Objective**
Diagnosed structural failures in an OLS model predicting AI software revenue using 2026 Nvidia AI capital expenditure and deployment data, applying HC3 robust standard errors to recover honest statistical inference.

**Methodology**
- Fit a naive OLS model on AI software revenue as a function of capital expenditure and deployment metrics, establishing a baseline for diagnostic comparison
- Conducted residual diagnostics to detect heteroscedasticity, identifying a pronounced variance expansion pattern concentrated at high capex tiers
- Audited for multicollinearity via variance inflation factors to isolate compounding sources of model instability
- Re-estimated the model using HC3 heteroscedasticity-consistent standard errors, correcting artificially deflated p-values without discarding observations or transforming the dependent variable

**Key Findings**
Naive OLS produced severely underestimated standard errors at high capital expenditure levels, generating false statistical confidence in several deployment coefficients. Correcting with HC3 estimators appropriately widened standard errors, materially shifting significance assessments and revealing which deployment metrics carry genuine predictive signal. The results underscore a common failure mode in technology sector regressions: high-value observations cluster in a way that systematically violates homoscedasticity, making robust inference not optional but necessary.
