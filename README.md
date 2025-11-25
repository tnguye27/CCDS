## Project Overview
This project investigates how **socioeconomic factors influence eviction filing rates across metropolitan and non-metropolitan jurisdictions in Maryland from 2000–2018**.  
Using data primarily from the Eviction Lab at Princeton University and supplementary Maryland county-level datasets, the study explores whether socioeconomic stressors have different effects in metropolitan versus non-metropolitan areas.  
The analysis follows the Quantitative Social Science Research (QSSR) track structure: data cleaning, exploratory data analysis (EDA), hypothesis testing, and model building.

## Progress Summary (Sprint 1–2)

### Data Collection and Cleaning
- Imported and merged datasets from the Eviction Lab and Maryland crime statistics (2000–2018).
- Verified data consistency and temporal alignment across sources.
- Confirmed that the final dataset has no missing values; Eviction Lab used a Bayesian hierarchical model combining court and LexisNexis data to estimate missing filings.
- Filtered the crime dataset to match the time frame and aggregated multiple offense types into a single *total crime* variable by county-year.
- Created a binary metropolitan variable:
  - `1` = Metropolitan (Frederick, Prince George’s, Montgomery)
  - `0` = Non-metropolitan (all others)
- Documented potential aggregation bias and outlier influence due to differences in income, crime, and eviction rates.

---

### Exploratory Data Analysis (EDA)

#### Univariate Analysis
- Grouped variables by year and metropolitan status; calculated mean values for each socioeconomic variable.
- Created time-series line plots.
- Key trends:
  - Non-metropolitan areas have higher mean poverty rates.
  - Metropolitan areas have higher median household income, eviction rates, and crime rates.
  - Rent burden remains similar between groups.
  - Metropolitan jurisdictions have lower mean percentage of white residents, consistent with literature on racial eviction disparities.
- Outliers identified:
  - High poverty (>20%) in some non-metropolitan jurisdictions.
  - High income (> $100,000) in Montgomery jurisdiction.
  - Elevated eviction and crime rates in select metropolitan jursidictions.

#### Bivariate / Multivariate Analysis
- Created scatterplots and correlation matrices for all independent variables vs. dependent variable, eviction filing rate.
- Observed expected relationships:
  - Positive: poverty, rent burden, crime rate, households threatened.
  - Negative: median household income, percent of population that is white.
- Metropolitan group showed stronger relationships between poverty and eviction, indicating greater sensitivity to economic stress in urban housing markets.

---

## Hypothesis Testing Framework
- Tested correlations between key socioeconomic indicators and eviction filing rates by metropolitan status.
- Observed how relationships vary by metropolitan status.
- Implement two-way fixed effects regression models (county and year fixed effects).
- Add interaction terms between socioeconomic variables and metropolitan status.
- Cluster standard errors at the county level to account for within-county correlation.
- Conduct diagnostics for multicollinearity, heteroskedasticity, and serial correlation.

## Progress Summary (Sprint 3)

Sprint 3 focused on building, evaluating, and interpreting fixed-effects regression models to understand how socioeconomic factors relate to eviction filing rates across Maryland counties from 2000–2018.

### Model Development
Created log-transformed variables for income, poverty, crime, and eviction filing rate to stabilize variance and improve interpretability.
Constructed a two-way fixed effects (county and year) regression model to control for unmeasured jurisdiction and year effects.
Added a poverty × metropolitan interaction term to test whether socioeconomic effects differ between metropolitan and non-metropolitan jurisdictions.
Implemented cluster-robust standard errors at the jurisdiction level to correct for heteroskedasticity and within-jurisdiction serial correlation.

### Key Findings
Crime rate (log_crime) is consistently a strong, statistically significant predictor of higher eviction filing rates.
Percent white is also statistically significant, with higher white population share associated with lower eviction activity.
Poverty, income, and rent burden are not statistically significant once fixed effects are included.
The poverty × metropolitan interaction is not significant, indicating that poverty’s effect on evictions does not meaningfully differ between metropolitan and non-metropolitan jurisdictions in this dataset.
Model fit is extremely high (R² ≈ 0.976), and coefficients are stable across specifications, suggesting robust associations but not causal effects.

### Model Diagnostics & Validation
Conducted assumption checks:
Linearity: relationships appear approximately linear when visualized using scatterplots and smoothing lines.
Normality: residuals show mild skew but approximate normality.
Heteroskedasticity: mitigated through clustered standard errors.
Independence: FE + clustering address within-cluster correlation.
Checked multicollinearity using Pearson correlations and VIF:
log_income and log_poverty show high correlation (–0.81), reducing interpretability of individual coefficients.

### Interpretation & Limitations
Models show strong associations, not causal effects.
Internal validity limited by:
Unmeasured confounders (landlord behavior, court efficiency, housing market tightness)
Potential measurement error in crime and poverty data
Possible reverse causality between crime, poverty, and evictions
External validity is limited to Maryland counties during 2000–2018.
