# Data Wrangling & Engineering Pipeline

## Objective
Engineer a production-ready feature matrix from a structurally compromised HR economics dataset by systematically diagnosing missingness patterns, resolving multicollinearity constraints, and compressing high-cardinality categorical variables — positioning the data for rigorous downstream econometric estimation.

---

## Methodology

- **Missingness Diagnosis (MAR Mapping):** Leveraged `missingno` to visualize and characterize the missingness architecture of `messy_hr_economics.csv`. Confirmed a Missing At Random (MAR) mechanism by identifying systematic co-occurrence patterns across variables, ruling out MCAR and informing imputation strategy selection.

- **Multicollinearity Mitigation — Dummy Variable Trap:** Applied one-hot encoding to nominal categorical features via `pandas`, enforcing reference class dropping (`drop_first=True`) to eliminate perfect linear dependence among indicator columns. This ensures full-rank design matrices compatible with OLS and related estimators in `statsmodels`.

- **High-Cardinality Encoding — Target Encoding:** Replaced raw geographic identifiers with target-encoded representations using `category_encoders.TargetEncoder`, substituting each region with its conditional mean of the outcome variable. This compresses sparse, high-dimensional geography into a single informative continuous feature without introducing prohibitive dimensionality.

- **Pipeline Integration:** Sequenced all transformations into a reproducible preprocessing pipeline, preserving a clean audit trail from raw data ingestion through engineered feature output.

---

## Key Findings

The dataset exhibited a **MAR missingness structure**, confirming that values were not missing at random with respect to all variables — a critical distinction that invalidates naive listwise deletion and motivates model-based or conditional imputation.

Strict enforcement of the **reference class constraint** successfully neutralized the Dummy Variable Trap, producing a full-rank regressor matrix and ensuring identifiability of all estimated coefficients.

**Target Encoding** proved an effective dimensionality reduction strategy for geographic variables: by anchoring encodings to outcome-conditional means, the transformation preserves the economic signal embedded in location while collapsing cardinality to a tractable scale.

The resulting feature matrix is structurally sound, econometrically compliant, and ready for regression modeling.

---

**Stack:** Python · pandas · statsmodels · missingno · category_encoders  
**Data:** `messy_hr_economics.csv`
