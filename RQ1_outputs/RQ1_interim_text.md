## 5. Analysis — RQ1: Branch coverage and banking deserts

    **Data cleaning.** We restricted scope to the 51 U.S. jurisdictions (50 states + DC), padded county keys to a 5-digit FIPS, coerced numeric fields, and joined all analyses to the canonical county dimension. Coverage is computed as **branches per 10,000 residents** using office counts aggregated from SOD and ACS population. Counties with population < 1,000 are flagged to avoid unstable ratios.

    **EDA.** Across **3,122 counties**, the mean coverage is **4.10**, median **3.22**, with a range **0.39 – 31.66** branches per 10k. 
    Counties with the **lowest** coverage include:
    - 45.0, UT: 0.39 branches per 10k
- 39.0, SC: 0.48 branches per 10k
- 79.0, NC: 0.49 branches per 10k
- 170.0, AK: 0.54 branches per 10k
- 79.0, MI: 0.55 branches per 10k

    The **highest** coverage examples include:
    - 77.0, NE: 31.66 branches per 10k
- 15.0, NE: 29.34 branches per 10k
- 75.0, SD: 29.13 branches per 10k
- 45.0, TX: 24.53 branches per 10k
- 95.0, ND: 23.66 branches per 10k

    By state, **lowest average coverage**: **AZ** (1.25); **highest**: **NE** (10.69).

    **Minimum sample size.** With ~3,122 counties and ≈5 predictors, the OLS rule of thumb (N ≥ 50 + 8p ≈ 90) is easily satisfied—our sample provides substantial power.

    **Interpretation of figures.** The histogram in `figs/hist_coverage.png` shows a right-skewed distribution: most counties have modest coverage, with a small group of highly-served counties forming a long tail.

    ## 6. Modelling

    **Model.** We regress county coverage on **median income, poverty rate, unemployment rate, % bachelor’s, and log(population)**, and include **state fixed effects** to absorb unobserved state-level differences.

    **Significance and direction.** Signs and p-values for the main effects:
    - Constant: ↑ coef=15.20, p=0.000***
- Median income: ↓ coef=-0.00, p=0.000***
- Poverty rate: ↓ coef=-0.05, p=0.000***
- Unemployment rate: ↓ coef=-0.11, p=0.000***
- % Bachelor’s+: ↑ coef=0.07, p=0.000***
- log(Population): ↓ coef=-1.02, p=0.000***

    **Feature engineering.** Coverage is per-capita (per 10k). Population is log-transformed to stabilize scale.

    ## 7. Preliminary results

    **Model performance.**
    - Baseline OLS: Adj. R²=0.419, RMSE=2.338, n=3083
- OLS + State FE: Adj. R²=0.602, RMSE=1.935, n=3083

    **Takeaways.** Coverage is **higher** in counties with higher incomes and education, and **lower** where poverty and unemployment are higher (holding state effects constant). The model fit (Adj. R²) indicates a meaningful share of cross-county variation is explained by these fundamentals.
