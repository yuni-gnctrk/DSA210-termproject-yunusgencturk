# F1 AeroMetrics: ATR Impact on The Competitiveness 
## Project Overview
This projects aims to investigate the relationship between Formula 1 competitiveness and the Aerodynamic Testing Regulations(ATR), implemented since the 2021 season. The ATR system which limits the wind tunnel time on sliding scale inverse to the Constructors Championship ranking, was introduced to increase the overall quality of the competition by narrowing down the gap between the team performances. By analyzing year-over-year lap time delta and the constructors' championship point gap among different years we aim to prove that the 2021 update on the regulations increases the competitiveness of the sport. The hypothesis will be: The ATR(Aerodynamic Testing Regulations) works as intended. Teams with greater wind-tunnel time improves at a faster rate.
## Motivation
As a passionate follower of the Formula 1 World Championship, I always wanted a more competitive sport since most of the time the results can be gussed by the middle of the season. FIA(Federation Internationale de l'Automobile) tries new regulations so i wanted to see if it has a impact or not. In this study i aim to improve my data analaysis skills through modeling, visualization and analysis.

### . Hypothesis 
**H₁:** Mean gap decreased Post-ATR → **T-Test, Levene's Test**  
**H₂:** Field spread variance decreased → **ANOVA, F-Test**  
**H₃:** Position correlates with development → **Pearson Correlation**  
**H₄:** ATR allocation correlates with development → **Linear Regression, ANOVA**

## Hypothesis Result
 **H₁ ACCEPTED:** Mean gap to pole decreased significantly from Pre-ATR (2017-2019) to Post-ATR (2022-2024) era  
 **H₂ ACCEPTED:** Year-to-year field variance decreased, indicating tighter competition  
 **H₃ REJECTED:** Championship position does NOT predict in-season development rate  
 **H₄ REJECTED:** ATR allocation does NOT correlate with development speed  

## Data Sources
Race and Qualifying Lap Times Data: For every race and qualifying session the data of the aravage pace and fastest lap for both drivers of every team is recorded: https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020/data

ATR times per team decided by the FIA starting from the 2021 season: Motorsport Technical Reports / FIA Docs

Official Constructor's Championship Points : Formula1.com

**Main Conclusion:** ATR regulations successfully leveled the field by constraining top teams' absolute performance (ceiling effect), NOT by accelerating bottom teams' development (no floor effect).

**Files Used:**
- `races.csv` - Race calendar and circuit information (2017-2024)
- `qualifying.csv` - Qualifying session lap times 
- `constructor_standings.csv` - Championship positions by race
- `constructors.csv` - Team names and identifiers

**Data Collection Method:**
- Downloaded Kaggle F1 Dataset
- Preprocessing: Converted lap times to seconds, filtered wet qualifying sessions
- Years analyzed: 2017-2019 (Pre-ATR), 2022-2024 (Post-ATR)
- Note: 2020 excluded due to COVID-19 regulation anomalies, 2021 marked as transition year

**Target Variable:** Gap to pole position (percentage)


###  Machine Learning: Linear Regression
**Model:** Multiple Linear Regression with StandardScaler  
**Features:** Previous gap metrics, championship position, development slope, ATR allocation, team tier  
**Target:** Next year's average gap to pole  
**Validation:** Time-aware split (2017-2022 train, 2023 test, 2024 validation)

**Why Linear Regression?**
- Course relative 
- Interpretable coefficients show direct ATR impact
- Appropriate for small dataset (~50 samples)
- Less prone to overfitting than complex models

###  2025 Performance Forecast
Predicted 2025 championship positions using 2024 data, then validated against actual 2025 season results.
