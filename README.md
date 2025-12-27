# F1 AeroMetrics: ATR Impact on Competitiveness

## Project Overview

This project investigates the relationship between Formula 1 competitiveness and Aerodynamic Testing Restrictions (ATR), implemented since the 2021 season. The ATR system limits wind tunnel time on a sliding scale inverse to Constructor's Championship ranking, introduced to increase competition quality by narrowing performance gaps between teams. By analyzing year-over-year qualifying lap time deltas and constructor championship standings across different eras, this study evaluates whether the 2021 regulation update successfully increased sport competitiveness.


## Motivation

As a passionate follower of Formula 1, I have long desired a more competitive sport, as race outcomes are often predictable by mid-season. The FIA (Fédération Internationale de l'Automobile) continually introduces new regulations to address this issue. This study allows me to analyze whether these regulations have a measurable impact while improving my data analysis skills through modeling, visualization, and statistical testing. Formula 1's data-driven engineering nature makes it an ideal subject for quantitative analysis. 

---

## Terminology (For Non-F1 Fans)

**ATR (Aerodynamic Testing Restrictions):** Regulations limiting wind tunnel and CFD (Computational Fluid Dynamics) testing time based on championship position. Lower-ranked teams receive more testing allocation (up to 115%), while top teams are restricted (as low as 70%).

**Qualifying:** Time trial sessions held before each race where drivers compete for starting grid positions by setting the fastest single lap time.

**Pole Position:** The first starting position on the grid, awarded to the driver/team with the fastest qualifying lap time.

**Gap to Pole:** Performance metric measuring the time difference (in seconds or percentage) between a team's best qualifying lap and the pole position lap.

**Constructor Championship Points:** Season-long points accumulated by teams based on race finishing positions, determining the Constructor's Championship standings.

**Big 4:** Historically dominant teams in Formula 1 - Mercedes, Ferrari, Red Bull, and McLaren - who have consistently competed at the front of the field.

---

## Hypotheses

### Primary Hypotheses (Competitiveness)

**Hypothesis 1: Performance Gap Reduction**
- H01 (Null): Mean gap to pole is EQUAL in Pre-ATR (2017-2019) vs Post-ATR (2022-2024) eras
- H11 (Alternative): Mean gap to pole DECREASED in Post-ATR era
- Statistical Tests: Independent t-test, Levene's test for equality of variances

**Hypothesis 2: Field Spread Reduction**
- H02 (Null): Year-to-year performance variance shows NO significant difference
- H12 (Alternative): Year-to-year performance variance DECREASED Post-ATR
- Statistical Tests: ANOVA (Analysis of Variance), F-test

### Secondary Hypotheses (Development Rate)

**Hypothesis 3: Championship Position vs Development**
- H03 (Null): NO correlation between championship position and in-season development rate
- H13 (Alternative): Lower championship positions (more ATR allocation) correlate with HIGHER development rates
- Statistical Test: Pearson correlation coefficient

**Hypothesis 4: ATR Allocation vs Development**
- H04 (Null): ATR allocation does NOT correlate with development speed
- H14 (Alternative): Higher ATR allocation correlates with FASTER in-season development
- Statistical Tests: Linear regression, ANOVA

---

## Data Sources

**Primary Dataset:** Kaggle Formula 1 World Championship Dataset (1950-2020+)  
**Source:** https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020/data

**Additional Data:**
- ATR allocation per team: FIA Technical Regulations / Motorsport Technical Reports
- Constructor Championship Points: Formula1.com official standings

**Files Used:**
- `races.csv` - Race calendar and circuit information (2017-2024)
- `qualifying.csv` - Qualifying session lap times 
- `constructor_standings.csv` - Championship positions by race
- `constructors.csv` - Team names and identifiers

**Data Collection Method:**
- Downloaded Kaggle F1 Dataset
- Preprocessing: Converted lap times to seconds, filtered wet qualifying sessions
- Years analyzed: 2017-2019 (Pre-ATR), 2022-2024 (Post-ATR)
- Note: 2020 excluded due to COVID-19 regulation anomalies; 2021 marked as transition year

**Target Variable:** Gap to pole position (percentage)

---

## Methodology

### 1. Data Collection & Preprocessing
- Extracted qualifying lap times (2017-2024)
- Converted time format to total seconds
- Filtered out wet sessions to isolate aerodynamic performance
- Standardized team names across years (e.g., "Force India" to "Aston Martin")

### 2. Exploratory Data Analysis
- Ridge plots showing gap distribution evolution over years
- Team performance heatmaps (2017-2024)
- Constructor championship points trends
- In-season development rate calculations (linear regression slopes per season)

### 3. Statistical Hypothesis Testing
- H1 & H2: Independent t-tests, ANOVA, Levene's test for equality of variances
- H3: Pearson correlation between championship position and development slope
- H4: Linear regression analyzing ATR allocation impact on development

### 4. Machine Learning: Linear Regression
**Model:** Multiple Linear Regression with StandardScaler  
**Features:** Previous gap metrics, championship position, development slope, ATR allocation, team tier  
**Target:** Next year's average gap to pole  
**Validation:** Time-aware split (2017-2022 train, 2023 test, 2024 validation)

**Why Linear Regression?**
- Interpretable coefficients show direct ATR impact
- Appropriate for small dataset (~50 samples)
- Less prone to overfitting than complex models

### 5. Model Validation
- Residual analysis to verify linear regression assumptions
- 5-Fold cross-validation to ensure model stability
- 2025 championship position predictions validated against actual season results

---

## Hypothesis Testing Results

The significance level was set to alpha = 0.05 for all statistical tests.

---
### Hypothesis 1: Performance Gap Reduction (Primary)

**Test:** Independent t-test comparing Pre-ATR (2017-2019) vs Post-ATR (2022-2024) mean gaps to pole

- **Pre-ATR Mean Gap:** 2.47%
- **Post-ATR Mean Gap:** 1.82%
- **t-statistic:** 4.23
- **p-value:** < 0.001
- **Levene's Test (Variance Equality):** p = 0.0341
- **Effect Size (Cohen's d):** 1.18 (large effect)
- **Conclusion:** REJECT H01 (Significant)

**Interpretation:** There is a statistically significant reduction in mean gap to pole from Pre-ATR to Post-ATR era. The competitive field has narrowed considerably, with the average performance gap decreasing by approximately 0.65 percentage points (26% reduction). This supports the hypothesis that ATR regulations successfully reduced performance disparities.

---

### Hypothesis 2: Field Variance Reduction (Primary)

**Test:** ANOVA comparing year-to-year gap variance

- **Pre-ATR Variance (avg):** 1.34
- **Post-ATR Variance (avg):** 0.89
- **F-statistic:** 8.76
- **p-value:** 0.0023
- **Conclusion:** REJECT H02 (Significant)

**Interpretation:** Year-to-year field spread variance decreased significantly in the Post-ATR era. The tightening of performance variance indicates more consistent competition across the field, with fewer extreme performance outliers. This demonstrates that ATR regulations achieved their goal of creating a more balanced competitive environment.

---

### Hypothesis 3: Championship Position vs Development Rate (Secondary)

**Test:** Pearson correlation between final championship position and in-season development slope

**Pre-ATR Era (2017-2019):**
- **Pearson's r:** -0.036
- **p-value:** 0.848
- **Relationship Direction:** Negligible negative
- **Conclusion:** FAIL to reject H03

**Post-ATR Era (2022-2024):**
- **Pearson's r:** -0.060
- **p-value:** 0.755
- **Relationship Direction:** Negligible negative
- **Conclusion:** FAIL to reject H03

**Interpretation:** Championship position does NOT predict in-season development speed in either era. Lower-ranked teams (who receive more ATR allocation) do not develop significantly faster than top teams. This suggests that organizational efficiency and technical capability matter more than wind tunnel time allocation.

---

### Hypothesis 4: ATR Allocation vs Development Speed (Secondary)

**Test:** Linear regression and ANOVA analyzing ATR allocation's effect on development rate

**Direct ATR Effect Test:**
- **Low ATR (70-85%, top teams):** Mean development = 0.0055
- **Medium ATR (85-100%):** Mean development = 0.0045
- **High ATR (100-115%, bottom teams):** Mean development = 0.0054
- **p-value (ANOVA):** 0.7545
- **R-squared:** 0.0035 (0.35% variance explained)
- **Conclusion:** FAIL to reject H04

**Interpretation:** ATR allocation explains only 0.35% of development variance. Teams with 70% ATR (e.g., Red Bull) develop at similar rates as teams with 115% ATR (e.g., Alpine). This finding, combined with H3 results, reveals that ATR regulations achieve competitiveness through constraint of leaders (ceiling effect) rather than empowerment of followers (no floor effect).

---

## Key Findings Summary

### Primary Findings

1. **ATR Regulations Are Effective**
   - Mean gap to pole decreased 26% from Pre-ATR to Post-ATR
   - Field variance reduced significantly (p = 0.0023)
   - Performance distribution tightened across all teams

2. **Mechanism: Ceiling Effect, Not Floor Effect**
   - ATR works by limiting top teams (Red Bull, Mercedes)
   - Does NOT accelerate bottom teams' development (H3, H4 rejected)
   - Organizational efficiency matters more than wind tunnel time

3. **Policy Implications**
   - ATR should continue to constrain leaders
   - Additional support needed for bottom teams beyond testing allocation
   - Development capability depends on team infrastructure, not just ATR

### Machine Learning Performance

**Linear Regression Model:**
- Training R-squared: 0.80-0.92 (strong fit on historical data)
- Test R-squared: 0.40-0.52 (moderate predictive power)
- MAE: ~0.5% gap prediction error
- Cross-validation: MAE = 0.562% ± 0.087% (stable across folds)

**2025 Validation:**
- Predicted championship order vs actual: 7/10 teams within ±2 positions
- McLaren P1 prediction: Correct (actual P1)
- Model successfully captured competitive trends despite F1's inherent volatility

---

## Limitations & Future Work

### Limitations

1. **Small Dataset:** ~50 team-year observations limit model complexity
2. **External Factors:** Cannot fully capture driver changes, technical breakthroughs, or organizational shifts
3. **Linear Assumptions:** Model assumes linear relationships between features
4. **COVID-19 Impact:** 2020 season excluded due to regulation anomalies

### Future Work
1. **Track Characteristics:** In Formula 1, some tracks require being faster on the straights (like Monza - these can be categorized as fast tracks), while others require better acceleration after slow turns rather than pure speed (like Monaco - these can be categorized as slow tracks). This difference leads to different aerodynamic features; therefore, the effect of ATR can also change across circuit types.
maybe:
2. **Expanded Features:** Include race pace data, not just qualifying performance
3. **Alternative Models:** Test polynomial regression for non-linear relationships

---

## Technologies Used

- Python 3.12
- Pandas, NumPy - Data manipulation
- Matplotlib, Seaborn - Visualization
- Scikit-learn - Machine learning (Linear Regression, StandardScaler, Cross-validation)
- SciPy - Statistical testing (t-test, ANOVA, Pearson correlation, Shapiro-Wilk)
- Jupyter Notebook

---



## References

1. Kaggle F1 Dataset - https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020
2. FIA Technical Regulations 2022-2024
3. Formula 1 Official Website - https://www.formula1.com


