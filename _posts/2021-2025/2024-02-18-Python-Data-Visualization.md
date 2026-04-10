---
layout: post
title: "Data Visualization with Python"
date: 2024-02-18
tags: [Data Science, Projects]
description: "In this project, I practice exploring data visualization with Python."
og_image: /assets/images/2021-2025/python-data-visualization/data-visualization-with-python.jpg
---
*Note: This is a project I completed for U.T. Austin's [Post Graduate Program in AI & Machine Learning: Business Applications](https://onlineexeced.mccombs.utexas.edu/online-ai-machine-learning-course){:target="_blank"}. The data and business scenarios are part of a simulated case study and do not represent the actual operations of any real-world entity.*

---

## Project Overview
My goal for this project was to get hands-on practice visualizing data using Python.  

## Setup
To begin, I imported the Python libraries I will use for this project:
- Pandas for managing the data.
- Matplotlib and Seaborn for visualizations. 

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## Understanding the Data
The data is a CSV file contaniing information on various automobiles (make, engine type, mpg, etc.). I imported the data into a pandas dataframe. 
```
df = pd.read_csv('/Automobile.csv')
```

To get a quick understanding of the data, I used the head(), shape(), info(), and describe() functions.

The head() function shows the first five rows by default. 
```
df.head()
>>>
```
![Automobile table head]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/automobile-table-head.webp)

The shape function tells me that the data consists of 201 rows and 26 columns. 
```
df.shape()
>>> (201,26)
```

The info() function displays the name, count, and data type for each column. 
```
df.info()
>>>
RangeIndex: 201 entries, 0 to 200
Data columns (total 26 columns):
 #   Column               Non-Null Count  Dtype  
---  ------               --------------  -----  
 0   symboling            201 non-null    int64  
 1   normalized_losses    201 non-null    int64  
 2   make                 201 non-null    object 
 3   fuel_type            201 non-null    object 
 4   aspiration           201 non-null    object 
 5   number_of_doors      201 non-null    object 
 6   body_style           201 non-null    object 
 7   drive_wheels         201 non-null    object 
 8   engine_location      201 non-null    object 
 9   wheel_base           201 non-null    float64
 10  length               201 non-null    float64
 11  width                201 non-null    float64
 12  height               201 non-null    float64
 13  curb_weight          201 non-null    int64  
 14  engine_type          201 non-null    object 
 15  number_of_cylinders  201 non-null    object 
 16  engine_size          201 non-null    int64  
 17  fuel_system          201 non-null    object 
 18  bore                 201 non-null    float64
 19  stroke               201 non-null    float64
 20  compression_ratio    201 non-null    float64
 21  horsepower           201 non-null    int64  
 22  peak_rpm             201 non-null    int64  
 23  city_mpg             201 non-null    int64  
 24  highway_mpg          201 non-null    int64  
 25  price                201 non-null    int64  
dtypes: float64(7), int64(9), object(10)
memory usage: 41.0+ KB
```
The describe() function provides statistical information for each colum (e.g. mean, standard deviation, quartiles, etc.)
![Automobile Data Description]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/automobile-data-description.webp)

## Visualizing the Data 

I used Seaborn to create graphs to visualize the data. 

### Histogram

The histplot() function produces a histogram. I used the 'price' column for the x axis, resulting in a histogram that groups the automobiles (the 201 rows) by price.  

```
sns.histplot(data=df, x='price')
```
![Price Histogram]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/price-histogram.webp)

I improved the appearance of the graph by including additional parameters (e.g. title, x and y axis labels, and custom coloring).

```
plt.title('Histogram: Price')
plt.xlim(3000,47000)
plt.ylim(0,70)
plt.xlabel('Price of Cars')
plt.ylabel('Frequency')
sns.histplot(data=df, x='price', color='orange')
```
![Price Histogram Improved]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/price-histogram-improved.webp)

I further enhanced the graph with information on body style. 
```
sns.histplot(data=df, x='price', kde=True, hue='body_style')
```
![Price Histogram Improved with Body Styles]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/price-histogram-improved-body-type.webp)

I used the FacetGrid() function to create price histograms for each body style. 

```
g = sns.FacetGrid(df, col="body_style")
g.map(sns.histplot, "price")
```
![Price Histogram Facet Grid]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/price-histogram-facetgrid-body-style.webp)

### Box Plot

I used the boxplot() function to create a box plot for each body style. 
```
sns.boxplot(data=df, x='body_style', y='price')
```
![Boxplot Body Styles]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/boxplot-body-styles.webp)

### Count Plot

Next, I wanted to see the distribution of car makes. I used the `countplot()` function to count the number of occurrences for each manufacturer. 

```python
sns.countplot(data=df, x='make')
```
![Countplot Car Makes]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/countplot-car-makes.webp)

Since the x-axis labels (the car makes) were overlapping and difficult to read, I adjusted the figure size and rotated the labels 90 degrees.

```python
plt.figure(figsize=(20,7))
sns.countplot(data=df, x='make', hue='make')
plt.xticks(rotation=90);
```
![Countplot Car Makes Improved]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/countplot-car-makes-improved.webp)

### Line Plot

To practice creating line plots, I briefly switched to some of Seaborn's built-in datasets. First, I loaded the "flights" dataset and plotted the number of passengers over time, using the `hue` parameter to color-code the lines by year. 

```python
flights = sns.load_dataset("flights")
sns.lineplot(data = flights, x = 'month', y = 'passengers', ci=False, hue='year');
```
![Flights Lineplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/flights-lineplot.webp)

Then, I loaded the "fmri" dataset. I used the `style` and `marker` parameters to further distinguish the lines representing different brain regions.

```python
frmi = sns.load_dataset("fmri")
sns.lineplot(data = frmi, x="timepoint", y="signal", hue="region", style="region", ci=False, marker=True)
```
![FMRI Lineplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/fmri-lineplot.webp)

## Exploring a New Dataset: Student Placement

To expand the scope of my project, I decided to import a second dataset. Since I was working in Google Colab, I mounted my Google Drive to access a CSV containing student placement data.

```python
drive.mount('/content/drive')
placement = pd.read_csv('/content/drive/MyDrive/Placement_Data.csv')
```

I started by getting a feel for the new data using the `head()` and `describe()` functions, just like I did with the automobile dataset. 

```python
placement.head()
>>>
```
![Placement Table Head]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/placement-table-head.webp)


```python
placement.describe()
>>>
```
![Placement Data Description]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/placement-data-description.webp)

I also created a quick count plot to see the ratio of students who were successfully placed versus those who were not, and used `value_counts()` to see the exact numbers.

```python
sns.countplot(data=placement, x = 'status',)
```
![Placement Status Countplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/placement-status-countplot.webp)

```python
placement['status'].value_counts()
>>>
```
![Placement Status Value Counts]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/placement-status-value-counts.webp)

## Advanced Visualizations

With the new dataset loaded, I experimented with slightly more complex visualizations to see how different academic metrics related to job placement.

### Comparing Academic Percentages

I used a histogram to map secondary education percentages (`ssc_p`) against higher secondary percentages (`hsc_p`), separated by placement status. 

```python
sns.histplot(data=placement, x='ssc_p', y='hsc_p', hue='status', kde=True)
```
![Academic Percentages Histogram]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/academic-percentages-histogram.webp)

I also used a line plot to look at this same relationship from a different visual perspective. 

```python
sns.lineplot(data=placement, x='hsc_p',y='ssc_p', hue='status')
```
![Academic Percentages Lineplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/academic-percentages-lineplot.webp)

### Heatmaps and Correlation

I wanted to explore the direct correlation between secondary and higher secondary percentages. I calculated the correlation and visualized it using a heatmap, setting `annot=True` to display the exact numerical values inside the grid.

```python
sns.heatmap(data=placement[['ssc_p','hsc_p']].corr(), annot=True);
```
![Simple Correlation Heatmap]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/simple-correlation-heatmap.webp)

Later, I generated a heatmap for the entire dataset's correlation matrix. I applied a custom color map (`cmap='YlGnBu'`) to make the stronger correlations visually pop.

```python
sns.heatmap(placement.corr(), annot = True, cmap='YlGnBu')
```
![Full Correlation Heatmap]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/full-correlation-heatmap.webp)

### Subject Streams and Degrees

I looked at the distribution of higher secondary subject streams (`hsc_s`) using a count plot.

```python
sns.countplot(x='hsc_s', data=placement, hue='hsc_s')
```
![Subject Stream Countplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/subject-stream-countplot.webp)

Then, I used a box plot to see how degree percentages (`degree_p`) varied across those different subject streams.

```python
sns.boxplot(data=placement, y='hsc_s', x='degree_p', hue='hsc_s' )
```
![Degree Percentage by Stream Boxplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/degree-percentage-stream-boxplot.webp)

To see how degree percentages directly affected placement status, I used a histogram with a kernel density estimate (`kde=True`).

```python
sns.histplot(data=placement, x='degree_p', hue='status', kde=True)
```
![Degree Percentage Status Histogram]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/degree-percentage-status-histogram.webp)

### Joint Plots and Hexbins

To see the relationship between employability test percentages (`etest_p`) and secondary percentages (`ssc_p`), I used a `jointplot()` with `kind='hex'`. A hexbin plot is incredibly useful for showing the density of overlapping data points.

```python
sns.jointplot(data=placement, x='etest_p', y='ssc_p', kind='hex')
```
![Employability vs Secondary Hexbin]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/employability-secondary-hexbin.webp)

I also viewed the employability test distribution on its own, noting the maximum score in the dataset.

```python
sns.histplot(data=placement, x='etest_p', kde=True)
placement['etest_p'].max()
>>> 98.0
```
![Employability Histogram]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/employability-histogram.webp)

### Linear Regression Plots

Finally, I used `lmplot()` to create a scatter plot with a linear regression line. This effectively mapped out the overarching trend between secondary and higher secondary scores, distinctly separated by placement status.

```python
sns.lmplot(x='ssc_p', y='hsc_p', hue='status', data= placement)
```
![Linear Regression Placement]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/linear-regression-placement.webp)

As a final check, I created a box plot to isolate secondary percentages and see their spread against the final placement status.

```python
sns.boxplot(x='ssc_p', y='status', data=placement)
```
![Secondary Percentage Status Boxplot]({{ site.baseurl }}/assets/images/2021-2025/python-data-visualization/secondary-percentage-status-boxplot.webp)