# Life Expectancy Prediction - Linear Regression

An end-to-end ML project predicting national life expectancy from varios indicators, using the WHO Life Expectancy Dataset off of Kaggle.

## Overview

The project walks through a full linear regression pipeline:
Exploratory data analysis, missing-value handling, outlier investigation, feature transformation, correlation-driven feature selection, model training and evaluation. 

## Dataset
- **Source:** [Life Expectancy (WHO) - Kaggle](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who)
- **Size:** ~2,900 rows, 193 countries, years 2000–2015
- **Target variable:** `Life expectancy`
- **Features used in the final model:**
  - "Schooling", "Income composition of resources", "GDP",
    "Diphtheria ", "Polio", " BMI ", "Total expenditure",
    "Alcohol", "Status", " thinness  1-19 years", " HIV/AIDS",
    "under-five deaths ", "Adult Mortality"

## Methodology
1. **EDA** — inspected shape, dtypes, missing-value percentages, and summary statistics.
2. **Outlier detection** — boxplots (log-scaled) on `GDP`, `Population`, and `under-five deaths`.
3. **Missing value handling** — per-column mean/median imputation, chosen based on skew and the proportion of missing data.
4. **Feature transformation** — log-transformed `GDP` and `Population` to correct skew; encoded `Status` (Developed/Developing) as binary.
5. **Correlation analysis** — built a full correlation matrix against the target, then checked correlation *among* candidate features to catch multicollinearity (e.g., `infant deaths` vs. `under-five deaths`, r ≈ 1.00 — one was dropped).
6. **Modeling** — 80/20 train/test split, `StandardScaler` for feature scaling, and `sklearn.linear_model.LinearRegression`.
7. **Evaluation** — R², MAE, RMSE, plus residual plots to check the model's assumptions.

## Results
 
| Metric | Value |
|--------|-------|
| R²     | 0.801 |
| MAE    | 3.32 years |
| RMSE   | 4.38 years |

**Strongest predictors:** `Adult Mortality` and `HIV/AIDS` (negative), `Schooling` (positive) — consistent with the correlation analysis and real-world expectations.

**Limitations:** residuals show mild heteroscedasticity and a few sizable outliers, suggesting
some relationships (e.g., GDP or schooling at extreme values) may not be perfectly linear.
Possible next steps include polynomial features or a regularized model (Ridge/Lasso).
 
## Project Structure
 
```
.
├── lifeExpectancyLinearReg.ipynb
├── README.md
└── requirements.txt
```
 
## Setup
 
```bash
git clone https://github.com/A-Rahil/lifeExpectancyLinearReg.git
cd lifeExpectancyLinearReg
pip install -r requirements.txt
jupyter notebook lifeExpectancyLinearReg.ipynb
```
 
## Tools
 
Python, pandas, NumPy, seaborn, matplotlib, scikit-learn
 
## Author
 
*Ahmed Rahil*