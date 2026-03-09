# Spurious Correlation & Multicollinearity in Macroeconomic Time-Series

## Overview
Investigated the pitfalls of naive correlation analysis in macroeconomic data by systematically diagnosing and resolving spurious relationships in raw FRED time-series. This project demonstrates why raw level data misleads, how to detect it, and how to recover true structural relationships.

## Methodology
1. **Data Collection** — Pulled macroeconomic indicators via the FRED API
2. **Visualization** — Used seaborn to expose correlation traps in non-stationary level data
3. **VIF Diagnostics** — Applied Variance Inflation Factor analysis via statsmodels to quantify multicollinearity and flag redundant predictors
4. **Transformation** — Converted non-stationary variables to Year-over-Year (YoY) growth rates to achieve stationarity
5. **Causal Mapping** — Constructed Directed Acyclic Graphs (DAGs) to recover true structural relationships obscured by shared trends

## Tech Stack
- **Language:** Python
- **Libraries:** pandas, seaborn, statsmodels
- **Data Source:** FRED API

## Key Takeaways
- Raw level correlations in macroeconomic data are almost always spurious
- VIF scores expose hidden multicollinearity invisible to standard correlation matrices
- YoY transformation is a lightweight, interpretable fix for non-stationarity
- DAGs force explicit reasoning about causality vs. correlation
