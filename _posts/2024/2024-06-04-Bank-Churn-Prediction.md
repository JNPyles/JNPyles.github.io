---
type: project
title: "Bank Churn Prediction Using a Neural Network Classifier"
date: 2024-06-04
category: [AI]
tags: [Complete,Python,Machine Learning]
description: "Building a neural network-based classifier that can determine whether a customer will leave the bank or not in the next 6 months."
excerpt: "Building a neural network-based classifier that can determine whether a customer will leave the bank or not in the next 6 months." 
image: /assets/images/2024-02-18-Python-Data-Visualization/data-visualization-with-python.jpg
---
## Context
Businesses like banks which provide services have to worry about the problem of 'Customer Churn' i.e., customers leaving and joining another service provider. It is important to understand which aspects of the service influence a customer's decision in this regard. Management can concentrate efforts on the improvement of service, keeping in mind these priorities.

## Objective
As a Data Scientist with the bank, the goal is to build a neural network-based classifier that can determine whether a customer will leave the bank or not in the next 6 months.

## Data Dictionary
* **CustomerId:** Unique ID which is assigned to each customer
* **Surname:** Last name of the customer
* **CreditScore:** It defines the credit history of the customer
* **Geography:** A customer’s location
* **Gender:** It defines the Gender of the customer
* **Age:** Age of the customer
* **Tenure:** Number of years for which the customer has been with the bank
* **NumOfProducts:** Refers to the number of products that a customer has purchased through the bank
* **Balance:** Account balance
* **HasCrCard:** It is a categorical variable which decides whether the customer has a credit card or not
* **EstimatedSalary:** Estimated salary
* **isActiveMember:** It is a categorical variable which decides whether the customer is an active member of the bank or not (Active member in the sense, using bank products regularly, making transactions etc.)
* **Exited:** Whether or not the customer left the bank within six months. It can take two values:
  * 0 = No (Customer did not leave the bank)
  * 1 = Yes (Customer left the bank)

---

## Setup and Importing Necessary Libraries

First, I installed the required packages and imported the necessary Python libraries for data manipulation, visualization, preprocessing, and model building.

```python
!pip install tensorflow==2.15.0 scikit-learn==1.2.2 seaborn==0.13.1 matplotlib==3.7.1 numpy==1.25.2 pandas==2.0.3 imbalanced-learn==0.10.1 -q --user

# Libraries for reading, manipulating, and visualizing data
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Library to split data
from sklearn.model_selection import train_test_split

# Library to standardise the data
from sklearn.preprocessing import StandardScaler, LabelEncoder

# Model building
import tensorflow as tf
from tensorflow import keras
from keras import backend
from keras.models import Sequential
from keras.layers import Dense, Dropout

# Importing SMOTE
from imblearn.over_sampling import SMOTE

# Importing metrics
from sklearn.metrics import confusion_matrix, roc_curve, classification_report, recall_score
import random

# Library to avoid warnings
import warnings
warnings.filterwarnings("ignore")
```

## Loading the Dataset

Since I worked in Google Colab, I mounted my Google Drive and loaded the CSV data into a Pandas DataFrame.

```python
from google.colab import drive
drive.mount('/content/drive')

data = pd.read_csv('/content/drive/MyDrive/machine_learning_project4/Churn.csv')
```

## Data Overview

I started by getting a high-level understanding of the dataset using standard Pandas functions.

```python
data.head()
data.tail()
data.shape
data.nunique()
data.info()
data.describe().T
data.isnull().sum()
data.duplicated().sum()
```

To clean the data, I dropped columns that wouldn't provide predictive value for the model.

```python
# Remove RowNumber, CustomerID, and Surname
data = data.drop(['RowNumber', 'CustomerId', 'Surname'], axis=1)
data.head()
```

### Observations
* There are 10,000 rows and 11 columns after removing the row number, customer ID, and surname columns.
* There are no missing values.
* There are no duplicate rows.

---

## Exploratory Data Analysis

### Univariate Analysis

```python
# Credit Score
plt.figure(figsize=(3, 5))
sns.boxplot(y=data['CreditScore'])
plt.title('Boxplot of CreditScore')
plt.show()

plt.figure(figsize=(5, 3))
sns.histplot(data['CreditScore'], bins=30, kde=True)
plt.title('Distribution of Credit Scores')
plt.xlabel('Credit Score')
plt.ylabel('Frequency')
plt.show()
```
**Credit Score Observations:**
* Credit score is mostly normally distributed, but slightly *left*-skewed.
* There is a sudden increase in frequency at the highest-end, which probably is due to credit scores having a maximum value, so the normal distribution is cut short and everything to the right of the cutoff is squeezed together.

```python
# Geography
plt.figure(figsize=(5, 3))
sns.countplot(x='Geography', data=data)
plt.title('Number of Entries per Country')
plt.xlabel('Country')
plt.ylabel('Count')
plt.show()
```
**Geography Observations:**
* There are three countries: France, Spain, and Germany.
* Spain and Germany each have around 2,500 rows.
* France has about 5,000 rows.

```python
# Gender
plt.figure(figsize=(5, 3))
sns.countplot(x='Gender', data=data)
plt.title('Gender')
plt.ylabel('Count')
plt.show()
```
**Gender Observations:**
* Approximately 4,500 rows are Female.
* Approximately 5,500 rows are Male.

```python
# Age
plt.figure(figsize=(3, 5))
sns.boxplot(y=data['Age'])
plt.title('Boxplot of Age')
plt.show()

plt.figure(figsize=(5, 3))
sns.histplot(data['Age'], bins=10, kde=True)
plt.title('Distribution of Ages')
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.show()
```
**Age Observations:**
* Age is normally distributed but skewed right.
* The majority of customers are in their 30s and 40s.

```python
# Tenure
plt.figure(figsize=(3, 5))
sns.boxplot(y=data['Tenure'])
plt.title('Boxplot of Tenure')
plt.show()

plt.figure(figsize=(5, 3))
sns.histplot(data['Tenure'], bins=10, kde=True)
plt.title('Distribution of Tenure')
plt.xlabel('Tenure')
plt.ylabel('Frequency')
plt.show()
```
**Tenure Observations:**
* Tenure ranges from 0 to 10.
* Except for tenures of 0 and 10, each other tenure is roughly equal, with about 1,000 rows.
* There are approximately 400 rows with 0 tenure.
* There are approximately 1,500 rows with 10 tenure.

```python
# Balance
plt.figure(figsize=(5, 3))
sns.histplot(data['Balance'], bins=30, kde=True)
plt.title('Distribution of Balances')
plt.xlabel('Balance')
plt.ylabel('Frequency')
plt.show()
```
**Balance Observations:**
* There is a very large portion of customers with an account balance of 0 - about 3,500.
* For customers that have a balance greater than 0, the balances are normally distributed, and most customers have a balance between 50,000 and 200,000.

```python
# Number of Products
plt.figure(figsize=(5, 3))
sns.countplot(x='NumOfProducts', data=data)
plt.title('Number of Products')
plt.xlabel('Country')
plt.ylabel('Count')
plt.show()
```
**Number of Products Observations:**
* Over 95% of customers purchased 1 or 2 products.
* Less than 5% purchased 3 products.
* About 1% purchased 4 products.
* The number of customers who purchased 1 product (about 5,000) is similar to the number of customers who purchased 2 products (about 4,600).

```python
# HasCrCard & Estimated Salary & IsActiveMember & Exited
plt.figure(figsize=(5, 3))
sns.countplot(x='HasCrCard', data=data)
plt.title('Has Credit Card')
plt.show()

plt.figure(figsize=(10, 3))
sns.histplot(data['EstimatedSalary'], bins=30, kde=True)
plt.title('Estimated Salaries')
plt.show()

plt.figure(figsize=(5, 3))
sns.countplot(x='IsActiveMember', data=data)
plt.title('Is an active member')
plt.show()

plt.figure(figsize=(5, 3))
sns.countplot(x='Exited', data=data)
plt.title('Customers that exited the bank within 6 months')
plt.show()
```
**Additional Observations:**
* Approximately 3,000 customers do not have credit cards, while 7,000 do.
* Salaries are nearly equally distributed from 0 to 200,000.
* A little more than half the customers are active members.
* Approximately 20% (2,000) of customers exited the bank within 6 months.

---

### Bivariate Analysis

First, I created a helper function to easily plot stacked bar charts comparing our categorical features against our target variable (`Exited`).

```python
# function to plot stacked bar chart
def stacked_barplot(data, predictor, target):
    """
    Print the category counts and plot a stacked bar chart

    data: dataframe
    predictor: independent variable
    target: target variable
    """
    count = data[predictor].nunique()
    sorter = data[target].value_counts().index[-1]
    tab1 = pd.crosstab(data[predictor], data[target], margins=True).sort_values(
        by=sorter, ascending=False
    )
    print(tab1)
    print("-" * 120)
    tab = pd.crosstab(data[predictor], data[target], normalize="index").sort_values(
        by=sorter, ascending=False
    )
    tab.plot(kind="bar", stacked=True, figsize=(count + 1, 5))
    plt.legend(
        loc="lower left",
        frameon=False,
    )
    plt.legend(loc="upper left", bbox_to_anchor=(1, 1))
    plt.show()
```

#### Correlation
```python
cols_list = ["CreditScore","Age","Tenure","Balance","EstimatedSalary"]
plt.figure(figsize=(15, 7))
sns.heatmap(data[cols_list].corr(), annot=True, vmin=-1, vmax=1, fmt=".2f", cmap="Spectral")
plt.show()
```
* **Observation:** The features exhibit almost no correlation with each other (all near 0).

#### Categorical Comparisons

```python
# Exited vs Geography
stacked_barplot(data, "Geography", "Exited" )

# Exited vs Gender
stacked_barplot(data, "Gender", "Exited" )

# Exited vs Has Credit Card
stacked_barplot(data, "HasCrCard", "Exited" )

# Exited vs Is Active Member
stacked_barplot(data, "IsActiveMember", "Exited" )
```

**Observations:**
* **Geography:** Customers in Germany are more likely to exit (~30%) than customers in Spain and France (~20%).
* **Gender:** Females are somewhat more likely to exit than males.
* **Credit Card:** Having a credit card has almost no impact on churn.
* **Active Member:** Active members appear to be less likely to exit than non-active members.

#### Numeric Comparisons

```python
# Exited vs Credit Score
plt.figure(figsize=(5, 3))
sns.boxplot(x='Exited', y='CreditScore', data=data)
plt.title('Credit Score vs. Customer Churn')
plt.show()

# Exited vs Age
plt.figure(figsize=(5, 3))
sns.boxplot(x='Exited', y='Age', data=data)
plt.title('Age vs. Customer Churn')
plt.show()

# Exited vs Balance
plt.figure(figsize=(5, 3))
sns.boxplot(x='Exited', y='Balance', data=data)
plt.title('Balance vs. Customer Churn')
plt.show()
```

**Observations:**
* **Credit Score:** The distribution is very similar, though nearly all customers with scores < 400 exited.
* **Age:** Customers who left tend to be older than customers who stayed.
* **Balance:** Customers who exited tend to have slightly higher balances.
* **Products:** 100% of customers with 4 products exited, and ~83% with 3 products exited. Customers with 2 products were the least likely to exit (~8%).

---

## Data Preprocessing

### Dummy Variable Creation
I converted the categorical variables into dummy/indicator variables.
```python
data = pd.get_dummies(data,columns=data.select_dtypes(include=["object"]).columns.tolist(),drop_first=True,dtype=float)
data.info()
```

### Train-Validation-Test Split
I split the data into 60% training, 20% validation, and 20% testing sets.
```python
X = data.drop(['Exited'],axis=1) # Independent variables
y = data['Exited'] # Dependent variable

# Splitting the dataset into the Training and Testing set (80/20)
X_large, X_test, y_large, y_test = train_test_split(X, y, test_size = 0.2, random_state = 42, stratify=y, shuffle = True)

# Split the 'large' dataset into training and validation sets (60/20 overall)
X_train, X_val, y_train, y_val = train_test_split(X_large, y_large, test_size=0.25, random_state=42, stratify=y_large, shuffle=True)

print(X_train.shape, X_val.shape, X_test.shape)
print(y_train.shape, y_val.shape, y_test.shape)
```

### Data Normalization
```python
# Creating an instance of the standard scaler
sc = StandardScaler()

# Fit the scaler on the training data and transform all splits
X_train[cols_list] = sc.fit_transform(X_train[cols_list])
X_val[cols_list] = sc.transform(X_val[cols_list])
X_test[cols_list] = sc.transform(X_test[cols_list])
```

---

## Model Building

### Model Evaluation Criterion
Given the business objective, we want to minimize false negatives so the bank can target customers who might leave. Since we are more interested in true positives, **Recall** is the best metric. A high recall indicates a model that successfully identifies most customers who are likely to leave.

```python
# Function for plotting the confusion matrix
def make_confusion_matrix(actual_targets, predicted_targets):
    """To plot the confusion_matrix with percentages"""
    cm = confusion_matrix(actual_targets, predicted_targets)
    labels = np.asarray(
        [
            ["{0:0.0f}".format(item) + "\n{0:.2%}".format(item / cm.flatten().sum())]
            for item in cm.flatten()
        ]
    ).reshape(cm.shape[0], cm.shape[1])

    plt.figure(figsize=(6, 4))
    sns.heatmap(cm, annot=labels, fmt="")
    plt.ylabel("True label")
    plt.xlabel("Predicted label")

# Two blank dataframes that will store the recall values for the models
train_metric_df = pd.DataFrame(columns=["recall"])
valid_metric_df = pd.DataFrame(columns=["recall"])
```

### Model Iterations

I built several Artificial Neural Network (ANN) architectures using Keras, experimenting with different optimizers (SGD vs. Adam), Dropout layers to prevent overfitting, and SMOTE to handle the class imbalance.

*(Note: For brevity, I've consolidated the code structure representing the final and best-performing architecture)*

#### The Best Model: Neural Network with SMOTE, Adam, and Dropout

To handle the imbalance in churners vs. non-churners, I applied SMOTE (Synthetic Minority Over-sampling Technique) to the training data.

```python
# Initialize SMOTE
sm = SMOTE(random_state=42)

# Fit SMOTE on the training data
X_train_smote, y_train_smote = sm.fit_resample(X_train, y_train)
```

Then, I built a deep neural network utilizing the Adam optimizer and Dropout layers.

```python
backend.clear_session()
np.random.seed(2)
random.seed(2)
tf.random.set_seed(2)

# Initializing the model
model_5 = Sequential()

# Input layer with Dropout
model_5.add(Dense(64, activation='relu', input_dim=X_train_smote.shape[1]))
model_5.add(Dropout(0.2))

# Hidden layers with Dropout
model_5.add(Dense(32, activation='relu'))
model_5.add(Dropout(0.1))
model_5.add(Dense(8, activation='relu'))

# Output layer
model_5.add(Dense(1, activation='sigmoid'))

# Compiling the model with Adam optimizer
from tensorflow.keras.optimizers import Adam
optimizer = Adam(learning_rate=0.001)
metric = keras.metrics.Recall()

model_5.compile(loss='binary_crossentropy', optimizer=optimizer, metrics=[metric])

# Fitting the ANN
history_5 = model_5.fit(
    X_train_smote, y_train_smote,
    batch_size=32,
    epochs=50,
    verbose=1,
    validation_data=(X_val, y_val)
)
```

## Final Model Selection & Evaluation

Comparing the models, the architecture utilizing SMOTE, Adam, and Dropout yielded the best results on the validation set.

```python
print("Training performance comparison")
print(train_metric_df)

print("Validation set performance comparison")
print(valid_metric_df)
```

**Test Set Evaluation:**
```python
# Best model is NN with SMOTE, Adam, and Dropout
y_test_pred = model_5.predict(X_test)
y_test_pred = (y_test_pred > 0.5)

# Print classification report & confusion matrix
cr = classification_report(y_test, y_test_pred)
print(cr)
make_confusion_matrix(y_test, y_test_pred)
```

---

## Actionable Insights and Business Recommendations

### Insights:
* We selected a neural network with SMOTE, Adam, and Dropout as the best model for predicting whether a customer will leave the bank within the next six months.
* The model is effective at identifying **73%** of customers who are likely to churn.
* When the model predicts a customer will churn, it is correct 49% of the time. This suggests there are some false positives, where customers are predicted to churn but do not.

### Recommendations:
1. **Targeted Retention:** Use the model to identify customers at high risk of churning and target them with retention strategies such as personalized offers, discounts, or loyalty programs.
2. **Personalized Outreach:** Reach out to high-risk customers with personalized communication to understand their needs and address any issues they might have.
3. **Investigate Product Churn:** Conduct further data analysis to identify common features of customers who churn. For example, the EDA showed that 100% of customers with four products churned. This may indicate a specific product suite issue that drives customers away.
4. **Feedback Loop:** Implement feedback mechanisms to gather insights from customers predicted to churn. Understanding their pain points can help improve services.
5. **Continuous Monitoring:** Regularly monitor the model's performance and update it with new data to ensure it remains accurate and effective over time.