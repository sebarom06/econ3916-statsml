Data Wrangling & Engineering Pipeline
Objective
Architect a production-grade data preparation pipeline that diagnoses and resolves structural missingness, eliminates multicollinearity artifacts, and encodes high-cardinality categorical features to produce an econometrically sound feature matrix ready for inferential modeling.

Methodology

Missingness Forensics — Deployed missingno matrix visualization to identify the structural alignment of null gaps across bonus_pay and performance_rating, classifying the underlying mechanism as Missing at Random (MAR) rather than MCAR or MNAR.
Conditional Median Imputation — Addressed MAR-driven gaps in base_salary via grouped imputation using pandas .groupby().transform(), computing within-department medians to preserve categorical variance structures rather than collapsing to a global statistic
Dummy Variable Trap Diagnosis — Intentionally constructed a full-rank dummy matrix (k categories, no reference class dropped) and confirmed singular matrix failure under OLS via statsmodels, empirically demonstrating the mechanism of perfect linear dependence.
Reference Class Encoding (k−1 Methodology) — Re-specified the design matrix using drop_first=True to establish an implicit reference category, resolving multicollinearity and producing an identified OLS model with stable coefficient estimates.
Target Encoding for High-Cardinality Features — Compressed an 80-level office_zip categorical variable into a single continuous vector using category_encoders.TargetEncoder, replacing each ZIP code with its conditional mean salary to retain geographic signal without dimensionality explosion.


Key Findings
Visual forensics confirmed that missingness in bonus_pay was structurally conditioned on performance_rating — a textbook MAR pattern that invalidates listwise deletion as a remediation strategy. Grouped median imputation preserved between-department salary distributions without introducing global bias. The Dummy Variable Trap experiment produced a rank-deficient design matrix, validating the theoretical basis for the k−1 encoding rule. The final OLS specification — incorporating tenure, department dummies (reference class dropped), and a target-encoded ZIP vector — yielded a fully identified model with interpretable marginal effects and no multicollinearity warnings.
