# AI Capex Diagnostic Modeling
 
## Objective
Diagnose structural violations of the Gauss-Markov theorem—specifically heteroscedasticity and multicollinearity—in an OLS regression predicting AI Software Revenue from 2026 Nvidia capital expenditure data, and apply HC3 Robust Standard Errors to eliminate false statistical confidence produced by the naive model.
 
---
 
## Data
**Nvidia AI Capital Expenditure & Deployment Dataset (2026)**
Synthetic dataset capturing high-dimensional technology sector activity across three predictors:
- `Hardware_Capex` — capital expenditure on AI hardware infrastructure
- `Data_Center_Power_MW` — data center power consumption in megawatts
- `Cloud_GPU_Deployments` — volume of cloud-based GPU deployments
 
**Target variable:** `AI_Software_Revenue`
 
---
 
## Methodology
 
### 1. Baseline OLS (The Illusion)
- Fit a naive OLS regression using `statsmodels` formula API
- Documented deceptively high R² and artificially low p-values — a false signal of model perfection
 
### 2. Visual Forensics
- Plotted residuals against fitted values using `seaborn`
- Identified a pronounced cone-shaped fan pattern, the canonical visual signature of heteroscedasticity
 
### 3. White Test (Formal Diagnosis)
- Extracted the model's internal design matrix via `model.exog`
- Passed residuals and design matrix into `het_white()` to statistically confirm that error variance is a function of the predictors
- Rejected the null hypothesis of homoscedasticity
 
### 4. Variance Inflation Factor (VIF) Analysis
- Iterated over the design matrix columns (skipping the intercept at index 0) using `variance_inflation_factor()`
- Quantified the degree of multicollinearity among predictors
- Ensured the constant column was present in the design matrix to avoid mathematically inflated VIF scores
 
### 5. HC3 Robust Standard Error Correction
- Re-fit the identical OLS formula using `.fit(cov_type='HC3')`
- Applied the heteroscedasticity-consistent HC3 sandwich estimator to recalibrate standard errors
- Compared naive vs. robust summaries to expose which variables lost significance once false confidence was removed
 
---
 
## Key Findings
- The naive OLS model exhibited severe heteroscedasticity concentrated at high capital expenditure tiers, causing standard errors to be systematically understated and p-values artificially deflated
- White Test results confirmed the violation with statistical significance, corroborating the visual diagnosis
- VIF analysis revealed meaningful multicollinearity between hardware and deployment metrics, consistent with the correlated nature of infrastructure scaling
- After applying HC3 correction, several previously "significant" predictors lost significance — not a model failure, but an accurate recalibration of true inferential confidence
 
---
 
## Tech Stack
`Python` · `pandas` · `statsmodels` · `matplotlib` · `seaborn`
