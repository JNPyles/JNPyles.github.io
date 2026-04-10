---
layout: post
title: "Machine Learning to Identify Bank Customers Interested in a Personal Loan"
date: 2024-04-13
tags: [Data Science, Projects]
description: "This is a machine learning project I completed for U.T. Austin's Post Graduate Program in AI & Machine Learning."
og_image: assets/images/2021-2025/machine-learning-targeted-marketing/machine-learning-to-identify-bank-customers-interested-in-a- personal-loan.jpg
---
*Note: This is a project I completed for U.T. Austin's [Post Graduate Program in AI & Machine Learning: Business Applications](https://onlineexeced.mccombs.utexas.edu/online-ai-machine-learning-course){:target="_blank"}. The data and business scenarios are part of a simulated case study and do not represent the actual operations of any real-world entity.*
---

## Executive Summary

### Context
The subject of this analysis is a US-based financial institution with a robust customer base of depositors (liability customers). While the bank maintains a steady flow of deposits, the segment of customers who also hold loan products (asset customers) remains small. To drive revenue through interest income, the bank’s management is focused on converting existing liability customers into personal loan holders while ensuring high retention of their current deposits.

A previous marketing campaign achieved a 9% conversion rate. To build on this success, this project leverages machine learning to identify high-probability prospects, allowing for more efficient, targeted marketing spend and a higher success ratio.

### Objective
* **Predictive Modeling**: Develop a classification model to predict whether a liability customer will accept a personal loan offer.
* **Feature Importance**: Identify the key demographic and financial attributes that drive loan purchases.
* **Strategic Segmentation**: Provide actionable recommendations for the marketing department to optimize future campaign targeting.

### Data Dictionary
* **Age/Experience**: Demographic markers of professional maturity.
* **Income**: Annual income ($1,000s).
* **Family**: Total family size.
* **CCAvg**: Average monthly credit card spend ($1,000s).
* **Education**: Level (1: Undergrad; 2: Graduate; 3: Advanced/Professional).
* **Mortgage**: Existing house mortgage value ($1,000s).
* **Personal_Loan**: Target Variable (0: No, 1: Yes).
* **Auxiliary Accounts**: Securities, CD accounts, Online banking, and external credit card usage.

---

## 1. Environment Setup & Data Acquisition

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

from sklearn.preprocessing import MinMaxScaler
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.tree import DecisionTreeClassifier, export_text, plot_tree
from sklearn.metrics import (
    f1_score,
    accuracy_score,
    recall_score,
    precision_score,
    confusion_matrix,
    make_scorer,
)

warnings.filterwarnings("ignore")

# Data ingestion
loan_data = pd.read_csv('Loan_Modelling.csv')
df = loan_data.copy()
```

## 2. Data Integrity & Cleaning

The dataset consists of 5,000 observations. We performed standard cleanup, including the removal of non-predictive identifiers and correcting logical inconsistencies in the `Experience` feature.

```python
# Removing ID as it holds no predictive weight
df = df.drop(["ID"], axis=1)

# Correcting negative 'Experience' values to absolute values
df['Experience'] = df['Experience'].abs()

# Verification of data types and null counts
print(df.info())
```

---

## 3. Exploratory Data Analysis (EDA)

### Critical Findings
* **The Income Threshold**: `Income` is the most significant differentiator. Customers accepting loans typically fall into higher income brackets compared to those who do not.
* **Education Premium**: Customers with Graduate or Professional degrees show a significantly higher conversion rate (approx. 13%) compared to undergraduates (<5%).
* **Credit Utilization**: Monthly credit card spending (`CCAvg`) shows a moderate positive correlation with loan acceptance, suggesting that high-utilization customers are prime candidates for liquidity products.

```python
# Visualizing the relationship between Income, Education, and Loan Acceptance
plt.figure(figsize=(10, 6))
sns.boxplot(x='Education', y='Income', hue='Personal_Loan', data=df)
plt.title('Income Distribution by Education and Loan Acceptance')
plt.show()
```

---

## 4. Feature Engineering & Preprocessing

To capture geographic influence, we mapped `ZIP Code` prefixes to California’s major economic regions.

```python
def map_regions(zip_code):
    prefix = str(zip_code)[:2]
    mapping = {
        '90': 'Los Angeles', '91': 'Pasadena', '92': 'San Diego',
        '94': 'SF Bay Area', '95': 'San Jose'
    }
    return mapping.get(prefix, 'Other California')

df['Region'] = df['ZIPCode'].apply(map_regions)
df = pd.get_dummies(df, columns=['Region'], drop_first=True)
df.drop(['ZIPCode'], axis=1, inplace=True)

# Train-Test Split (80/20)
X = df.drop('Personal_Loan', axis=1)
y = df['Personal_Loan']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
```

---

## 5. Predictive Modeling: Decision Trees

We utilized a Decision Tree Classifier due to its high interpretability—a critical requirement for banking stakeholders who need to justify marketing logic.

### Optimization Strategy
We compared three iterations of the model:
1. **Base Model**: Highly complex, exhibiting signs of overfitting.
2. **Pre-Pruned**: Optimized via `GridSearchCV` for maximum recall.
3. **Post-Pruned (Selected)**: Utilized Cost-Complexity Pruning (`ccp_alpha`) to create a robust, generalized model.

```python
# Final Model: Post-Pruned Decision Tree
final_model = DecisionTreeClassifier(
    ccp_alpha=0.01, 
    class_weight={0: 0.15, 1: 0.85}, 
    random_state=1
)
final_model.fit(X_train, y_train)
```

---

## 6. Model Evaluation

| Metric | Training Set | Test Set |
| :--- | :--- | :--- |
| **Accuracy** | 98.1% | 97.5% |
| **Recall** | 90.1% | 89.6% |
| **Precision** | 90.3% | 85.6% |

**Evaluation Logic**: In a loan campaign, **Recall** is our primary metric. We want to ensure we capture as many potential "Yes" responders as possible, even at the cost of slight precision loss (mailing a few "No" responders).

---

## 7. Actionable Insights & Business Strategy

### Marketing Targets
* **The "High-Value" Segment**: Prioritize customers with an annual income > $110k and Graduate-level education. This group represents the highest conversion probability.
* **Debt Consolidation**: Customers with high `CCAvg` but no mortgage may be seeking to consolidate revolving debt. Tailor messaging to emphasize lower interest rates compared to credit cards.

### Strategic Compliance & Risk
* **Fair Lending Awareness**: While targeting high-income/highly-educated segments is effective, the bank must ensure marketing practices do not inadvertently exclude protected classes.
* **Refinement Loop**: Implementation of this model should include a "Champion-Challenger" test phase to validate the model's performance against a random control group in the next campaign.

### Feature Importance
The visualization below confirms that `Income`, `Education`, and `Family Size` are the primary drivers of the model's decisions.

```python
# Plotting Feature Importances
importances = final_model.feature_importances_
indices = np.argsort(importances)
plt.figure(figsize=(8, 8))
plt.title("Feature Importances")
plt.barh(range(len(indices)), importances[indices], color="steelblue")
plt.yticks(range(len(indices)), [X_train.columns[i] for i in indices])
plt.show()
```