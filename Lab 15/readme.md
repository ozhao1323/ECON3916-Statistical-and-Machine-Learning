
---

## The Polynomial Trap: Bias-Variance Tradeoff
`Python` `NumPy` `scikit-learn` `Matplotlib`

This lab investigates how model complexity governs the bias-variance tradeoff through controlled experiments on both synthetic and real-world data. Using 50 training and 200 test observations drawn from a noisy sine-wave process, the analysis traces MSE curves across polynomial degrees, identifying the optimal complexity window at degrees 3–5 — the region where approximation error and variance are jointly minimized. Critically, cross-validation selected the same degree range as held-out test performance, validating CV as a reliable model-selection heuristic without access to test labels.

The analysis extends to the Ames Housing dataset (1,460 observations, 80 features), where a parsimonious 5-feature polynomial model outperformed a kitchen-sink specification in cross-validated RMSE despite yielding lower training R². This result concretely illustrates a phenomenon common in applied econometrics and industry modeling: a model that memorizes training noise generalizes poorly, while disciplined feature selection recovers predictive signal.

Together, these experiments build the methodological case for complexity regularization in production models. The notebook demonstrates fluency with the full scikit-learn pipeline — feature engineering, K-fold CV, and diagnostic visualization — applied to both clean experimental conditions and the messiness of real housing data.

---

