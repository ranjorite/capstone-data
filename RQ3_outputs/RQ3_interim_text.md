## 5. Analysis — RQ3: Deposit concentration (latest year = 2024)

**a. Data cleaning.** Scope fixed to the **51 jurisdictions** (50 states + DC), standardized county **FIPS**, and joined to the canonical county dimension. From the merged SOD+ACS file we kept only required fields and coerced numerics. Counties with **offices = 0** were excluded for concentration; counties with **pop < 1,000** were flagged.

**b. EDA results.** We analyze **3109** counties overall; the regression sample has **3104** counties (complete features). Target is **log(deposits per branch)**; distribution plot: `RQ3/output/figs/hist_log_dep_per_branch.png`. Correlations among features and target are in `rq3_correlation_matrix.csv`; multicollinearity checks in `rq3_vif.csv`.

**c. Minimum sample size.** OLS heuristic **N ≥ 50 + 8p** is easily satisfied (thousands of counties vs ~5 predictors + state FE).

**d. Interpretation of figures.** Deposit concentration is right-skewed; log-transform stabilizes variance. Higher **income** and **education** tend to align with higher concentration; **poverty**/**unemployment** align with lower concentration.

**e. Insights.** County-level rankings of predicted concentration (FE model) identify hot-spots for high/low deposit concentration.
Top examples:
- New Castle County, DE: predicted=1,005,205, observed=2,598,877
- Sussex County, DE: predicted=786,664, observed=1,875,346
- Kent County, DE: predicted=696,185, observed=112,954
- District of Columbia, DC: predicted=349,293, observed=349,293
- Los Angeles County, CA: predicted=347,334, observed=351,999

Bottom examples:
- Issaquena County, MS: predicted=26,329, observed=13,601
- Hooker County, NE: predicted=26,554, observed=48,784
- Loup County, NE: predicted=28,054, observed=33,980
- Hayes County, NE: predicted=28,322, observed=28,685
- Thomas County, NE: predicted=29,182, observed=30,141

---

## 6. Modelling

**a. Model and features.** Outcome: **log(deposits per branch)**. Predictors: `median_income`, `poverty_rate`, `unemployment_rate`, `% bachelors`, `log(pop)`, with **state fixed effects**.

**b. Justification.** Socio-economic indicators and market size are expected to drive deposit concentration; state FE absorb institutional/policy differences.

**c. Outputs.** Coefficients: `rq3_model_baseline_coeffs.csv`, `rq3_model_fe_coeffs_main.csv`. Metrics: `rq3_model_metrics.csv`.

---

## 7. Preliminary results

**Model performance.** 
- Baseline OLS: Adj. R² = 0.450 | RMSE (log) = 0.417 | n = 3104
- OLS + State FE: Adj. R² = 0.500 | RMSE (log) = 0.394 | n = 3104

**Takeaway.** Deposit concentration is **higher** in counties with higher education and income, and **lower** where poverty and unemployment are higher, controlling for state effects. Effect sizes and p-values are reported in the coefficient tables; FE specification materially improves fit.
