# Hypothesis Testing & Causal Evidence Architecture

## Project: The Epistemology of Falsification — Hypothesis Testing on the Lalonde Dataset

---

## Objective

Most applied analytics workflows are optimized for *estimation* — producing a number. This project
pivots to *falsification* — stress-testing whether that number means anything. Using the Lalonde
(1986) experimental dataset, I operationalized the scientific method as a formal evidence
architecture, adjudicating between competing causal narratives around the effectiveness of job
training programs. The central question was not "what is the effect?" but "can we trust that the
effect is real?"

---

## Technical Approach

- **Signal-to-Noise Decomposition via Welch's T-Test:** Framed the Average Treatment Effect (ATE)
as a signal-to-noise problem. The observed $1,795 lift in real earnings constitutes the signal; the
pooled variance across groups defines the noise floor. Welch's formulation was selected over
Student's T to avoid the assumption of homogeneous variance — a common failure mode in income
distribution data.

- **Non-Parametric Validation via Permutation Testing:** Earnings distributions are notoriously
non-normal (zero-inflated, right-skewed). To guard against parametric assumptions corrupting the
inference, I ran a 10,000-resample permutation test using `scipy.stats.permutation_test`. This
simulates the null world — one where treatment labels are meaningless — and empirically derives a
p-value from first principles rather than a theoretical distribution.

- **Type I Error Governance:** Maintained a strict α = 0.05 decision threshold throughout. Both
the parametric and non-parametric tests produced consistent p-values, providing convergent validity
and confirming the result is not an artifact of distributional assumptions.

---

## Key Finding

The Null Hypothesis — that job training had no effect on 1978 real earnings — was rejected. The
~$1,795 Average Treatment Effect clears the significance threshold under both testing regimes,
establishing causal evidence via *Proof by Statistical Contradiction*: the observed result is
sufficiently improbable under a world where the treatment does nothing.

---

## Business Insight: Hypothesis Testing as the Safety Valve of the Algorithmic Economy

In production data environments, the risk is never a *shortage* of patterns — it's a surplus of
them. With enough features and enough model iterations, spurious correlations are inevitable.
P-hacking, data dredging, and overfitting to noise are not edge cases; they are the natural
byproduct of optimization pressure applied without epistemic guardrails.

Rigorous hypothesis testing is the safety valve. By defining the null hypothesis before analysis,
pre-committing to a significance threshold, and validating parametric results against
non-parametric baselines, this workflow operationalizes *disciplined skepticism* — the same
principle that separates a reproducible scientific finding from a dashboard metric that collapses
under scrutiny. In an economy where algorithmic decisions govern credit, hiring, and resource
allocation, the cost of a false positive is not academic. Hypothesis testing is how we ensure that
what looks like signal *is* signal.

Netflix's Return-Aware Experimentation framework treats the significance threshold as a dynamic
business parameter calibrated to the cost asymmetry of each decision — a high-stakes, irreversible
change demands a stricter bar than a low-cost, easily-rolled-back tweak. This challenges the
academic default of p < 0.05, which applies a uniform threshold regardless of the economic
consequences of being wrong. The practical takeaway is that α is a risk budget, not a constant —
and every experiment design embeds an implicit business judgment that should be made explicitly.
