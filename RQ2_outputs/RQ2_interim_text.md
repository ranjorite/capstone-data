## 5. Analysis — RQ2: Decade change in branch networks (2015–2024)

**a. Data cleaning.** We restricted to the **51 jurisdictions** (50 states + DC), standardized county FIPS, and built a **county×year panel** from SOD with `offices` (unique UNINUMBR), `main_offices` (BKMO='Y'), `branches_only`, and **deposits**. Files: `RQ2/output/county_year_offices.(csv|xlsx)`; change table `county_change_2015_2024.(csv|xlsx)`.

**b. EDA results.** Histograms show distributions for **offices 2015**, **offices 2024**, **Δ offices**, and **% change** (`hist_offices_2015.png`, `hist_offices_2024.png`, `hist_delta_offices.png`, `hist_pct_change.png`).  
Average **% change in offices** across **3,118 counties**: **-12.69%**.

**Largest gains (Δ offices)**  
- Lincoln County, SD: Δ=12, %Δ=57.1%
- Collin County, TX: Δ=10, %Δ=4.0%
- Benton County, AR: Δ=10, %Δ=11.1%
- Walton County, FL: Δ=10, %Δ=40.0%
- Montgomery County, TX: Δ=8, %Δ=5.5%

**Largest losses (Δ offices)**  
- Cook County, IL: Δ=-379, %Δ=-25.0%
- Los Angeles County, CA: Δ=-365, %Δ=-20.3%
- Maricopa County, AZ: Δ=-207, %Δ=-24.5%
- New York County, NY: Δ=-170, %Δ=-24.3%
- Suffolk County, NY: Δ=-164, %Δ=-34.9%

**c. Minimum sample size.** OLS heuristic **N ≥ 50 + 8p** is easily met (thousands of counties vs a handful of predictors + state FE).

**d. Interpretation of figures.** The Δ-offices histogram indicates overall **network contraction** with pockets of growth; the change table highlights concentrated declines and some growth clusters.

**e. Insights.** Reporting both **absolute** (Δ) and **percent** changes avoids overstating swings in tiny-baseline counties.

---

## 6. Modelling

**a. Model and features.** Outcome: **% change in offices (2015→2024)**. Predictors: `log1p(offices_2015)`, `log1p(deposits_2015)`, plus **state fixed effects**. We winsorize the outcome (1%) to reduce extreme ratios from very small baselines.

**b. Justification.** Initial network scale and market size explain much of subsequent change; state FE controls for unobserved policy/regulatory differences.

**c. Outputs.** Coefficients: `regression_baseline_coeffs.csv`. Key metrics: `regression_key_metrics.json`.

---

## 7. Preliminary results

**Paired comparisons (2015 vs 2024).** Overall mean Δ = **-5.21** branches; **p-value = 1.797e-66**.  
Number of **states** with significant paired change (p < 0.05): **38**.

**Model performance (OLS with state FE).** Adj. R² = **0.218**, RMSE = **14.531**, n = **3090**.

**Takeaway.** Branch networks generally **contracted**, with the steepest declines concentrated in specific states and regions. Baseline scale variables explain a **meaningful but partial** share of the variation in county-level changes, after accounting for state effects.
