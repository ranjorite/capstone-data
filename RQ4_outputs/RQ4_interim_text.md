## 5. Analysis — RQ4: County-level predictors of bank failures (2015–2024)

**a. Data cleaning.** Scope: 50 states + DC. County keys padded to 5-digit **FIPS** and joined to the county dimension. From the combined FDIC workbook we mapped failures (2015–2024) to counties via **CERT → location**. Features from SOD+ACS were coerced to numeric and engineered: `poverty_rate`, `unemployment_rate`, `% bachelors`, `log_pop`.

**b. EDA results.** Class balance is highly skewed (failures are rare).
 We observe **30 fail** vs **3075 no-fail** counties.
 Descriptive contrasts:
- `log_pop` mean: **11.797 (fail)** vs **10.293 (no-fail)**
- `% bachelors` mean: **0.336 (fail)** vs **0.240 (no-fail)**
- `median_income` mean: **76301.167 (fail)** vs **66049.023 (no-fail)**
- `poverty_rate` mean: **0.137 (fail)** vs **0.142 (no-fail)**

**c. Minimum sample size.** Logistic EPV guideline is ≥10. Events per predictor (EPV) ≈ **6.00** (30 events, 5 predictors). Interpret coefficients with appropriate caution.

**d. Interpretation of figures.** The ROC curve (`RQ4/output/figs/rq4_roc.png`) shows moderate separability; the dashboard lists the highest-risk counties according to predicted probabilities.

---

## 6. Modelling

**a. Model & features.** Logistic regression on county **failure_flag** with predictors: `median_income`, `poverty_rate`, `unemployment_rate`, `% bachelors`, `log_pop`.

**b. Justification.** Socio-economic structure and market size plausibly relate to institutional stress; `log_pop` captures exposure (more banks → higher chance of any failure).

**c. Outputs.** `rq4_model_metrics.csv`, `rq4_logit_coeffs_odds.csv`, `rq4_high_risk_dashboard.csv`, and `figs/rq4_roc.png`.

---

## 7. Preliminary results

**Performance.** Accuracy = **0.990** | ROC-AUC = **0.695** | n = **3105**.

**Significant predictors (odds ratios).**
- **log_pop**: OR = **1.560**, p = **0.002**
- **pct_bachelors**: OR = **106.709**, p = **0.039**

**Highest-risk counties (model ranking, top 5).**
- Washington County, New York — predicted prob 18.3%
- Collier County, Florida — predicted prob 12.1%
- Hardin County, Illinois — predicted prob 11.7%
- Monterey County, California — predicted prob 11.5%
- Harris County, Georgia — predicted prob 11.1%