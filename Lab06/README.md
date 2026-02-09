# Lab 5: The Architecture of Bias

## Overview
Investigated the Data Generating Process (DGP) and Sampling Bias in machine learning pipelines. Demonstrated how sampling methodology directly impacts model validity and experimental integrity.

## Tech Stack
- **Python**: pandas, numpy, scipy, sklearn
- **Statistical Methods**: Chi-Square tests, Stratified Sampling

## Methodology

### 1. Simple Random Sampling
Manually simulated random sampling on the Titanic dataset to quantify natural sampling variance and demonstrate inherent sampling error in train/test splits.

### 2. Stratified Sampling
Implemented stratified sampling using `sklearn.model_selection.train_test_split` to preserve class distributions and eliminate Covariate Shift between training and test sets.

### 3. Sample Ratio Mismatch (SRM) Detection
Conducted forensic audit using `scipy.stats.chisquare` to detect systematic randomization failures in A/B test allocation. Distinguished between natural variance and engineering failures in treatment assignment.

## Theoretical Question: Survivorship Bias in Unicorn Analysis

**Problem**: Analyzing only successful Unicorn startups on TechCrunch creates Survivorship Bias because the dataset conditions on outcome (success). The sample excludes all failed startups that never reached unicorn status, creating a non-representative view of the true startup ecosystem.

**The Ghost Data**: To implement a Heckman Correction, you need data on the **selection mechanism itself**:

1. **All startups that attempted funding** (both successes and failures)
2. **Selection variables** that predict visibility/survival independent of true quality:
   - Founder network strength
   - Geographic location (proximity to VC hubs)
   - Media coverage propensity
   - Industry hype cycles
3. **Outcome variables** measured for both visible and invisible companies:
   - Revenue, burn rate, team size
   - Product metrics (if available pre-failure)

**Heckman's Two-Stage Process**:
- **Stage 1** (Selection Equation): Model P(being observed | characteristics) using probit regression on the full population
- **Stage 2** (Outcome Equation): Model success conditional on selection, correcting for correlation between selection and outcome errors (λ, the Inverse Mills Ratio)

Without data on failed/invisible startups, you cannot estimate the selection mechanism, and thus cannot correct for the bias introduced by conditioning on survival.
