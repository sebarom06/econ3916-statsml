# Recovering Experimental Truths via Propensity Score Matching

---

## Objective

Applied Propensity Score Matching (PSM) to correct for systematic selection bias in observational
data, recovering a credible causal estimate of job training's effect on earnings from a dataset
where naive comparison is structurally misleading.

---

## Methodology

- **Selection Bias Modeling:** Diagnosed the observational failure by identifying that the control
group in the CPS/PSID observational sample is drawn from a fundamentally different population than
the treated group — violating the exchangeability assumption required for valid causal inference.

- **Propensity Score Estimation:** Trained a logistic regression model on pre-treatment covariates
(age, education, race, prior earnings) to estimate each unit's conditional probability of receiving
treatment. This collapses a high-dimensional confounding problem into a single balancing score.

- **Nearest-Neighbor Matching:** Matched each treated unit to its closest control counterpart in
propensity score space, constructing a synthetic comparison group that approximates the
covariate balance of a randomized experiment.

---

## Key Findings

| Estimator | Treatment Effect |
|---|---|
| Naive Observational (Pre-Matching) | -$15,204 |
| PSM-Adjusted (Post-Matching) | ~+$1,800 |
| Lalonde Experimental Benchmark | ~+$1,795 |

The naive estimate — a negative $15,204 — is not noise. It is the signature of selection bias: the
observational control group systematically out-earns the treated group on pre-treatment
characteristics, making the raw comparison meaningless. Post-matching, the recovered treatment
effect converges to approximately +$1,800, achieving near-exact alignment with the experimental
ground truth established by the randomized benchmark. This validates PSM as a credible
bias-correction mechanism and demonstrates that with proper covariate adjustment, observational
data can recover causal estimates that rival those produced under random assignment.
