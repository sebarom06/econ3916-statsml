Statistical Analysis Assignment
This repository contains Python implementations for statistical audits covering robustness, probability, bias, and survivorship bias.
Files
Combined Script

all_phases_combined.py - Complete assignment in one file (recommended for notebooks)

Individual Scripts

phase1_step1_latency_trap.py - Simulates skewed latency data
phase1_step2_mad_vs_sd.py - Compares MAD vs Standard Deviation
phase2_bayesian_audit.py - Bayesian probability calculations
phase3_chi_square_srm.py - Chi-Square goodness of fit test
task4_memecoin_graveyard.py - Survivorship bias simulation with visualization

Output

memecoin_graveyard.png - Visualization comparing all tokens vs survivors

Requirements
pythonpandas
numpy
matplotlib
seaborn
Phase 1: The Robustness Audit
Step 1.1: The "Latency" Trap
Simulates 1,000 requests:

980 normal requests (20-50ms)
20 spike requests (1000-5000ms)

Key Finding: Mean (89.49ms) heavily skewed by outliers, median (36.00ms) shows typical performance.
Step 1.2: Manual MAD vs. SD
Implements calculate_mad() function to demonstrate robustness.
Key Finding:

SD: 406.71ms (45x larger than MAD)
MAD: 9.00ms (stable despite outliers)

Phase 2: The Probability Audit
Bayesian Audit - False Positive Paradox
Calculates P(Cheater|Flagged) for a "98% accurate" plagiarism detector.
Results:

Bootcamp (50% base rate): 98.00%
Econ Class (5% base rate): 72.06%
Honors Seminar (0.1% base rate): 4.68%

Key Insight: Even highly accurate tests produce mostly false positives when the condition is rare.
Phase 3: The Bias Audit
Chi-Square Goodness of Fit Test
Tests for Sample Ratio Mismatch (SRM) in A/B testing.
Data:

Control: 50,250 users
Treatment: 49,750 users

Result: χ² = 2.50 < 3.84 (critical value)
Conclusion: No significant bias detected, experiment is valid.
Task 4.1: The Memecoin Graveyard
Survivorship Bias Simulation
Simulates 10,000 token launches using Pareto distribution.
Key Findings:

All tokens mean: $47,650.34
Top 1% mean: $1,490,810.57
Survivorship bias multiplier: 31.29x

Insight: Analyzing only successful tokens inflates perceived returns by 31x, hiding the reality that 99% fail.
Usage
Run All Phases (Recommended)
pythonpython all_phases_combined.py
Run Individual Phases
pythonpython phase1_step1_latency_trap.py
python phase1_step2_mad_vs_sd.py
python phase2_bayesian_audit.py
python phase3_chi_square_srm.py
python task4_memecoin_graveyard.py
In Jupyter Notebook
python# Copy contents of all_phases_combined.py into a single cell
%run all_phases_combined.py
Key Concepts

Robust Statistics: MAD resists outliers better than SD
Base Rate Fallacy: Test accuracy depends heavily on condition prevalence
Sample Ratio Mismatch: Always check for bias before analyzing A/B tests
Survivorship Bias: Only analyzing successes gives false impression of typical outcomes

Output Format
All scripts produce minimal, clean output showing only essential results. Visualizations are saved as PNG files.
