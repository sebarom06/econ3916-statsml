# Tree-Based Models — Random Forests
### ECON 3916: Data Science for Economists | Lab 19

---

## Objective

Benchmark decision trees, Ridge regression, and Random Forests on the California Housing dataset to quantify the predictive gains from ensemble methods over linear baselines, and to critically evaluate feature importance measures as predictive — not causal — tools.

---

## Methodology

- **Data:** California Housing dataset (scikit-learn), 20,640 observations, 8 features
- **Train/test split:** 80/20, `random_state=42` throughout
- **Model comparison:** Unrestricted Decision Tree vs. Ridge (α=1.0) vs. Random Forest (100 trees) on RMSE and R²
- **Hyperparameter tuning:** GridSearchCV with 5-fold CV over `n_estimators` ∈ {50, 100, 200}, `max_depth` ∈ {10, 20, None}, `max_features` ∈ {'sqrt', 0.5, None}
- **Feature importance:** MDI (training-set, impurity-based) vs. permutation importance (test-set, model-agnostic)
- **Classification:** Binary target (above/below median price); RF Classifier vs. Logistic Regression evaluated on AUC-ROC
- **Interactive dashboard:** Plotly + ipywidgets; sliders for `n_estimators` and `max_features` updating model comparison, feature importance, and train/test R² in real time
- **Partial dependence plots:** Marginal effects of `MedInc` and `AveOccup` illustrating non-linearities captured by RF

---

## Key Findings

- The Random Forest achieves Test R² ≈ 0.81 vs. Ridge's ≈ 0.60, confirming the price-feature relationship is non-linear and cannot be adequately captured by a linear model
- The Single Decision Tree achieves near-perfect Train R² (≈ 1.00) but collapses to Test R² ≈ 0.62 — a textbook illustration of variance-dominated overfitting
- `MedInc` is the top predictor under both MDI and permutation importance; geographic features (Latitude, Longitude) are inflated by MDI due to high cardinality but rank lower under permutation importance
- Feature importance reflects predictive association, not causal effect: `MedInc`'s dominance reflects correlation with unmeasured amenities, not a causal income-to-price pathway
- Hyperparameter tuning yields modest but consistent improvement over default RF settings (~1–2 pp R² gain)
- RF Classifier achieves AUC ≈ 0.93–0.95 vs. Logistic Regression's ≈ 0.87–0.89 — a practically meaningful gap for real-estate classification tasks

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/your-username/econ-lab-19-random-forests.git
cd econ-lab-19-random-forests

# Install dependencies
pip install numpy pandas matplotlib scikit-learn plotly ipywidgets

# Launch notebook
jupyter notebook notebooks/lab-ch19-complete.ipynb
```

The interactive dashboard (AI Expansion section) requires a live Jupyter environment — it will not render as static HTML.

---

## Repository Structure

```
econ-lab-19-random-forests/
├── README.md
├── notebooks/
│   └── lab-ch19-complete.ipynb
├── figures/
│   ├── ch19_feature_importance.png
│   └── ch19_partial_dependence.png
└── verification-log.md
```

---

## Dependencies

| Package | Version |
|---|---|
| scikit-learn | ≥ 1.3 |
| numpy | ≥ 1.24 |
| pandas | ≥ 2.0 |
| matplotlib | ≥ 3.7 |
| plotly | ≥ 5.15 |
| ipywidgets | ≥ 8.0 |
