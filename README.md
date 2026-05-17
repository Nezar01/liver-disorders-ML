# 🍺 Predicting Alcohol Consumption from Liver Blood Tests
**BUPA Liver Disorders Dataset – Data Mining Project**  
TH Lübeck | Course: Data Management |  Nezar Alassaf

---

## Project Overview

This project investigates whether a person's alcohol consumption can be predicted from blood/liver test results. The well-known **BUPA Liver Disorders dataset** is used, which contains 5 laboratory values alongside daily alcohol intake.

---

## Dataset

- **Source:** [BUPA Liver Disorders Dataset (UCI)](https://archive.ics.uci.edu/ml/datasets/liver+disorders)
- **File:** `bupa.data`
- **345 samples**, 6 features (after dropping the `selector` column)

| Feature   | Description                          |
|-----------|--------------------------------------|
| `mcv`     | Mean corpuscular volume              |
| `alkphos` | Alkaline phosphatase                 |
| `sgpt`    | Alanine aminotransferase             |
| `sgot`    | Aspartate aminotransferase           |
| `gammagt` | Gamma-glutamyl transferase (GGT)     |
| `drinks`  | Alcohol consumption (half-pints/day) → **Target** |

---

## Methods

### 1. Exploratory Data Analysis (EDA)
- Statistical summary (`describe()`)
- Scatter plots: each feature vs. `drinks`
- Correlation analysis → `gammagt` has the strongest linear relationship (r ≈ 0.386)
- Standardization with `StandardScaler` + boxplot comparison before/after

### 2. Multiple Linear Regression
- All 5 liver values as features
- **R² ≈ 0.188** → model explains ~18.8% of variance in `drinks`
- Weak linear relationships throughout the dataset

### 3. Learning Curve
- Training with 10%, 20%, 40%, 80%, 100% of the data
- Result: 100% of training data yields the best R² on test data
- All R² values near 0 or negative → confirms weak linear structure

### 4. Polynomial Regression (on `gammagt`)
- Degrees 1, 2, and 3 compared
- R² ≈ 0.15 across all degrees → polynomial extension provides minimal improvement
- No overfitting detected (R² barely increases with degree)

### 5. Logistic Regression (Classification)
- Binary target: `drinks > 3` → heavy drinker (1) or not (0)
- **Train Accuracy: 0.69 | Test Accuracy: 0.60**
- 60% test accuracy is only slightly better than random guessing (50%)

---

## Results & Conclusion

- Liver blood test values alone are **not sufficient** to reliably predict alcohol consumption
- `gammagt` is the strongest single predictor, but still weak (r ≈ 0.39)
- Both regression (R² ≈ 0.19) and classification (Acc. ≈ 0.60) show limited predictive power
- Potential improvements: additional demographic features (age, weight), more complex models (Random Forest, XGBoost)

---

## Project Structure

```
liver+disorders/
├── bupa.data                      # Raw data
├── bupa.names                     # Feature descriptions
├── DM_Nezar_Alassaf_B1.ipynb      # Jupyter Notebook (main analysis)
├── requirements.txt               # Python dependencies
└── README.md                      # This file
