---
title: "Univariate and Multivariate Analysis of Food Delivery Service"
date: 2024-02-26
tags: [Data Science, Projects]
---
*Note: This is a project I completed for U.T. Austin's [Post Graduate Program in AI & Machine Learning: Business Applications](https://onlineexeced.mccombs.utexas.edu/online-ai-machine-learning-course){:target="_blank"}. The data and business scenarios are part of a simulated case study and do not represent the actual operations of any real-world entity.*

## Executive Summary

### Context
In the fast-paced environment of New York City, online food delivery services have become a staple for students and busy professionals. This analysis focuses on data from a major food aggregator that connects customers with multiple restaurants through a centralized smartphone app. The aggregator handles the end-to-end process: order placement, restaurant confirmation, delivery person assignment, and final drop-off. 

The company generates revenue by collecting a fixed margin from restaurants on every order. To improve customer experience and business efficiency, this study analyzes order patterns, restaurant demand, and delivery logistics.

### Objective
* **Demand Analysis**: Identify the most popular restaurants and cuisines to understand market trends.
* **Logistics Optimization**: Analyze food preparation and delivery times to refine customer expectations.
* **Financial Insights**: Calculate net revenue and identify high-value customer segments.
* **Customer Feedback**: Evaluate the current rating system and suggest improvements for better data collection.

### Data Dictionary
* **Order/Customer ID**: Unique identifiers for tracking transactions.
* **Restaurant Name/Cuisine Type**: Categorical data identifying the vendor and food style.
* **Cost**: Total cost of the order in USD.
* **Day of the Week**: Categorized as Weekday (Mon–Fri) or Weekend (Sat–Sun).
* **Rating**: Customer score (1–5 or "Not given").
* **Preparation Time**: Minutes from order confirmation to courier pick-up.
* **Delivery Time**: Minutes from courier pick-up to customer drop-off.

---

## 1. Environment Setup & Data Overview

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
df = pd.read_csv('foodhub_order.csv')

# Initial Data Inspection
print(f"Dataset Shape: {df.shape}")
print(df.info())

# Checking for missing values
print("Missing Values:\n", df.isnull().sum())
```

### Initial Observations
* The dataset contains **1,898 orders** across **9 columns**.
* There are **no missing values** (nulls) in the dataset; however, many ratings are marked as "Not given."
* **Preparation Time**: Ranges from 20 to 35 minutes, with an average of approximately 27 minutes.

---

## 2. Univariate Analysis: Key Distributions

We explored individual variables to understand the underlying patterns in customer behavior and operational performance.

```python
# Statistical summary of preparation time
df.describe()['food_preparation_time']

# Distribution of ratings
plt.figure(figsize=(6,5))
sns.countplot(data=df, x='rating', order=['3', '4', '5', 'Not given'])
plt.title('Distribution of Customer Ratings')
plt.show()

# Orders by Cuisine Type
plt.figure(figsize=(8,5))
sns.countplot(data=df, x='cuisine_type')
plt.title('Orders Per Cuisine Type')
plt.xticks(rotation=90)
plt.show()
```

### Key Findings from Univariate Exploration
* **Customer Loyalty**: Most customers have placed 3 or fewer orders. A small segment of "power users" (only 8 customers) has placed 4 or more orders.
* **Cuisine Popularity**: Japanese, American, Italian, and Chinese cuisines dominate the platform, accounting for over **80% of all orders**.
* **Weekly Trends**: Delivery volume on **weekends is more than double** the volume on weekdays, suggesting a strong "leisure" use case for the app.
* **Rating Gap**: Approximately **38% of customers (736 orders)** do not leave a rating. Curiously, there are no ratings of 1 or 2, which may indicate a technical limitation or a bias in the review solicitation process.

---

## 3. Multivariate Analysis: Understanding Correlations

To understand the drivers of cost and customer satisfaction, we analyzed the relationships between time, cost, and cuisine.

```python
# Correlation Heatmap
plt.figure(figsize=(10,5))
sns.heatmap(df.corr(), annot=True, cmap='Spectral')
plt.title('Variable Correlation Matrix')
plt.show()

# Total Time Calculation
df['total_time'] = df['food_preparation_time'] + df['delivery_time']

# Cost by Cuisine Type
plt.figure(figsize=(10,5))
sns.boxplot(data=df, x='cuisine_type', y='cost_of_the_order')
plt.title('Order Cost Distribution by Cuisine')
plt.xticks(rotation=90)
plt.show()
```

### Insights on Time and Cost
* **Delivery Efficiency**: The mean delivery time on weekdays is **28.3 minutes**, whereas weekends are significantly faster at **22.5 minutes**, likely due to different traffic patterns or courier availability.
* **Total Lead Time**: 11% of all orders take more than **60 minutes** from placement to delivery.
* **Revenue Generation**: Based on a tiered commission structure (25% for orders >$20; 15% for orders >$5), the total net revenue generated across the 1,898 orders was **$6,166.30**.

---

## 4. Strategic Business Questions

### High-Value Restaurant Partners
The top 5 restaurants by order volume are:
1.  **Shake Shack**
2.  **The Meatball Shop**
3.  **Blue Ribbon Sushi**
4.  **Blue Ribbon Fried Chicken**
5.  **Parm**

*Note: These 5 restaurants alone account for nearly one-third of the total order volume.*

### Promotional Eligibility
To qualify for a premium promotional offer, restaurants must have >50 ratings and an average rating >4. The qualifying restaurants are:
* **Blue Ribbon Fried Chicken**
* **Blue Ribbon Sushi**
* **Shake Shack**
* **The Meatball Shop**

---

## 5. Conclusions & Strategic Recommendations

### Conclusions
* **Revenue Concentration**: A tiny fraction of restaurants (less than 3%) drives a massive portion of the revenue. This presents both a success story and a risk of over-reliance on a few partners.
* **The Weekend Surge**: The platform is primarily a weekend service. Weekday lunch and dinner slots represent a significant underutilized capacity for the delivery fleet.
* **Feedback Limitations**: The lack of negative ratings (1–2 stars) and the high volume of "Not given" ratings suggests the feedback loop is broken or incomplete.

### Recommendations
1.  **Workplace Marketing**: Implement a "Weekday Lunch" campaign targeting office buildings and co-working spaces to balance the weekend-heavy order load.
2.  **Growth Support for Mid-Tier Restaurants**: Create "How to Grow" playbooks for restaurants with high ratings but low order volume, sharing best practices from top performers like Shake Shack.
3.  **Incentivized Ratings**: Offer small delivery discounts or "loyalty points" to customers who provide ratings, specifically aiming to reduce the "Not given" segment.
4.  **Expand Family-Sized Options**: Since most orders are currently between $10–$25, there is an opportunity to market "Family Bundles" or "Party Platters" to increase the average order value (AOV) above the $40 mark.
5.  **Data Enhancement**: Future iterations of this analysis should include **order dates** and **geographic data** (Zip Codes) to perform seasonal trend analysis and identify neighborhood-specific demand clusters.