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
