# NY Fed Yield Curve Recession Model Replication

## Objective
Replicated the Federal Reserve Bank of New York's yield curve recession model by fitting a logistic regression on FRED macroeconomic data to predict NBER-defined recessions 12 months ahead.

## Methodology
- **Data Collection:** Retrieved two FRED series via the `fredapi` Python client — the 10-Year minus 3-Month Treasury yield spread (T10Y3M, daily) and the NBER recession indicator (USREC, monthly), covering January 1970 to present
- **Data Processing:** Resampled the daily yield spread to month-end frequency and applied a 12-month lag to enforce genuine out-of-sample forecasting, matching the NY Fed's published model specification
- **Linear Probability Model (Baseline):** Fit an OLS regression on the binary recession indicator to demonstrate the core failure of the Linear Probability Model — out-of-bounds predicted probabilities below 0% and above 100% on real Federal Reserve data
- **Logistic Regression:** Fit a logistic regression using `scikit-learn` to produce a well-bounded sigmoid probability curve; extracted predicted recession probabilities using the `.predict_proba()[:,1]` pattern
- **Odds Ratio Extraction:** Re-estimated the model in `statsmodels` to obtain standard errors and 95% confidence intervals; exponentiated the yield spread coefficient to produce an interpretable odds ratio
- **Probability Time Series:** Applied the fitted model to the full dataset to generate a monthly recession probability time series with NBER recession shading, replicating the chart format published by the NY Fed

## Key Findings
- The Linear Probability Model produced logically impossible predicted probabilities on real data — confirming that OLS is unsuitable for binary outcomes in practice, not just in theory
- The logistic regression coefficient on the lagged yield spread is negative, confirming that a steeper yield curve is associated with lower recession risk and an inverted curve with elevated risk
- The odds ratio indicates that each 1 percentage-point increase in the yield spread meaningfully reduces the odds of recession within the following 12 months
- During the 2022–2024 yield curve inversion — the longest since the 1980s — the model assigned recession probabilities of 70–85%, yet no NBER recession materialized, illustrating that a high predicted probability is not equivalent to a certain outcome
- The model performed strongly in the 2006–2007 period, correctly assigning rising recession probabilities ahead of the 2008–2009 recession

## Tools & Technologies
- **Languages:** Python
- **Data:** FRED API (T10Y3M, USREC)
- **Libraries:** `pandas`, `numpy`, `scikit-learn`, `statsmodels`, `fredapi`, `matplotlib`, `plotly`
