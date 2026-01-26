# Project: Supervised Learning — Model Quality

## 📌 Project Description

The online store *“One Click”* faced a decline in purchasing activity among its existing customers. Attracting new users has become less effective, so the business needs a solution to **retain customers through personalized offers**.

As part of this project, a machine learning model was developed to predict the probability of a decline in customer purchasing activity. Based on the predicted risk and customer profitability, **customer segmentation** was performed and **practical business recommendations** were proposed.

---

## 🎯 Research Objectives

- Identify factors influencing the decline in purchasing activity.
- Build and compare several classification models.
- Select the best model using the **ROC-AUC** metric.
- Segment customers by risk of activity decline and profitability.
- Develop recommendations to increase activity in key segments.

---

## 📊 Data

Data from the online store were used:

- `market_file` — behavioral and marketing customer characteristics  
- `market_money` — monthly revenue  
- `market_time` — time spent on the website  
- `money` — average monthly profit per customer  

All tables were merged by `id`; data cleaning, typo correction, and feature standardization were performed.

---

## 🔧 Preprocessing and EDA

- Standardization of column names (`snake_case`)
- Cleaning of categorical values (typos, extra spaces)
- Analysis of distributions, outliers, and class imbalance
- Correlation analysis:
  - **Spearman** — for numerical features  
  - **Phik** — for mixed features (numerical + categorical)

---

## 🤖 Modeling

A unified `Pipeline` with `ColumnTransformer` was used:

- `OneHotEncoder` — for nominal categorical features  
- `OrdinalEncoder` — for ordered categorical features  
- `StandardScaler / MinMaxScaler / passthrough` — for numerical features  

Four models were trained and compared:

- `LogisticRegression (L1)`  
- `DecisionTreeClassifier`  
- `KNeighborsClassifier`  
- `SVC`  

Hyperparameter tuning was performed using **RandomizedSearchCV (cv=5)**.  
The primary metric was **ROC-AUC** (robust to class imbalance and suitable for risk ranking).

---

## ✅ Best Model

**LogisticRegression (L1, C = 3, solver = liblinear)**

- Mean ROC-AUC (CV): ≈ **0.898**  
- ROC-AUC on the test set: **0.923**  
- Significantly outperforms the baseline (DummyClassifier)

L1 regularization enabled informative feature selection and improved model interpretability.

---

## 🔍 Feature Importance Analysis

Three approaches were used:

- logistic regression coefficients (L1)
- SHAP values
- permutation importance (ROC-AUC)

Most influential factors:

- on-site engagement (pages per visit, category views, time spent)
- accumulated marketing activity
- share of promotional purchases and abandoned carts

---

## 📦 Customer Segmentation

Customers were segmented along two axes:

- **Risk of activity decline** (`p_drop ≥ 0.5`)
- **Profitability** (above / below the 75th percentile)

Four segments were identified:

- **HR–HP** — high risk, high profitability (priority segment)
- HR–LP
- LR–HP
- LR–LP

---

## 💡 Business Recommendations

Focus on the **HR–HP** segment:

- personalized recommendations for key categories
- reducing dependence on discounts (bonuses, cashback, service value)
- abandoned cart recovery
- post-purchase communications and engagement enhancement

This approach helps **maximize the economic impact of retention efforts**.

---

## 📁 Repository Structure

```text
supervised-learning/
├── data/
│   └── *.csv
├── notebooks/
│   └── supervised_learning.ipynb
├── README.md
└── .gitignore
