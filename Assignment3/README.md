# Econ_3916_Assignment_3_Causal

## Overview
Causal inference analysis investigating labor compensation and algorithmic fairness using SwiftCart gig economy data.

---

## Dependencies
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

## Steps

### Step 1.1 — Zero-Inflated Tip Distribution
Simulates 250 driver tips: 100 zero-tips + 150 drawn from Exponential(scale=5.0).

### Step 1.2 — Manual Bootstrap Engine
10,000 resamples of `driver_tips` to build a 95% bootstrap confidence interval for the median using `np.percentile`.

### Step 2.1 — A/B Test Data (Routing Algorithm)
500 Control deliveries from Normal(35, 5) and 500 Treatment deliveries from LogNormal(3.4, 0.4). Computes observed difference in means.

### Step 2.2 — Permutation Test
5,000 permutations of the combined delivery array to compute an exact empirical p-value for the routing algorithm A/B test.

### Step 3.1 — Naive SDO (Loyalty Program)
Loads `swiftcart_loyalty.csv`. Computes the naive Simple Difference in Means between SwiftPass subscribers (D=1) and non-subscribers (D=0).

### Step 3.2 — Propensity Score Matching (PSM)
Logistic regression on pre-treatment covariates (`pre_spend`, `account_age`, `support_tickets`) to estimate propensity scores. 1-to-1 nearest-neighbor matching to isolate the causal ATT.

### Task 4.1 — Love Plot
Standardized Mean Differences plotted before and after PSM to visualize covariate balance. Balance threshold at ±0.1 SMD.

---

## Data
- `swiftcart_loyalty.csv` — required for Steps 3.1, 3.2, and 4.1
  - `subscriber` — treatment indicator (1 = SwiftPass member)
  - `pre_spend` — pre-treatment monthly order volume
  - `account_age` — account age in months
  - `support_tickets` — historical support tickets filed
  - `post_spend` — post-treatment monthly spending (outcome)
