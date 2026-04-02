High-Dimensional GDP Growth Forecasting with Lasso and Ridge Regularization
Objective
Forecast 5-year average GDP per capita growth rates across 120+ countries using 36 World Development Indicators, while demonstrating the OLS overfitting failure mode in high-dimensional settings and applying Lasso and Ridge regularization with cross-validated penalty selection to improve out-of-sample generalization.
Data

Source: World Bank World Development Indicators (WDI) via the wbgapi Python API
Coverage: ~150 countries, 2013–2019 (pre-COVID)
Domains: Trade & openness, macroeconomics, education, infrastructure, health, finance, natural resources, agriculture, and governance
Structure: Annual panel collapsed to one cross-sectional observation per country via time-averaging; countries and indicators with >40% missing values dropped; remaining gaps imputed with cross-country medians

Methodology

Train–test split: Countries divided 70/30 to simulate out-of-sample generalization across economies
OLS baseline: Fit on standardized features to establish the overfitting benchmark; training and test R² recorded to quantify the train–test gap
Ridge regression (RidgeCV): L2 penalty shrinks all coefficients toward zero; optimal λ selected via 5-fold cross-validation over a log-spaced grid from 0.01 to 1,000
Lasso regression (LassoCV): L1 penalty drives a subset of coefficients to exactly zero, performing automatic feature selection; optimal λ selected via 5-fold cross-validation
Lasso Path: Computed via sklearn.linear_model.lasso_path to trace all coefficient estimates as λ varies from fully sparse to near-OLS, revealing the order in which predictors enter the model
Feature standardization: StandardScaler fit exclusively on training data and applied to test data to prevent data leakage

Tech Stack
Python · wbgapi · scikit-learn · pandas · numpy · matplotlib
Key Findings

OLS overfitting confirmed: With a predictor-to-observation ratio (p/n) exceeding 0.5, OLS achieved a training R² near 1.0 while test R² was substantially lower — a textbook case of variance explosion in high-dimensional cross-sectional data
Regularization closes the gap: Both RidgeCV and LassoCV significantly reduced the train–test R² gap, improving out-of-sample generalization without sacrificing meaningful predictive power
Lasso sparsity: LassoCV selected approximately 5–10 predictors out of 30+, identifying the subset of WDI indicators most robustly associated with cross-country growth
Lasso Path interpretation: The first predictors to enter the model at high penalty — those with the strongest marginal signal — were investment, institutional quality, and trade-related indicators, consistent with the cross-country growth literature
Predictive redundancy ≠ economic irrelevance: Zeroed-out predictors (e.g., paved_roads_pct, internet_users_pct) reflect conditional predictive redundancy given correlated covariates in the model, not evidence of economic insignificance
