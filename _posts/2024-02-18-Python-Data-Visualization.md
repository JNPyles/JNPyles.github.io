---
layout: project
title: "Python Data Visualization Practice"
date: 2024-02-18
category: [Python]
tags: [Complete,Python,Data Analytics]
github_url: "https://github.com/JNPyles/8-Bit-Breadboard-Computer-Project"
description: "Practice using Python's data visualization libraries, includiong Numpy, Pandas, Matplotlib, and Seaborn."
---

# Setup
To begin, I import the Python libraries I will use. 
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

# Understanding the Data
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
![Automobile table head]({{ site.baseurl }}/assets/images/2024-02-18-Python-Data-Visualization/automobile-table-head.webp)

```

The shape function tells me that the data consists of 201 rows and 26 columns. 

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
![Automobile Data Description]({{ site.baseurl }}/assets/images/2024-02-18-Python-Data-Visualization/automobile-data-description.webp)

## Visualizing the Data 

I used Seaborn to create graphs to visualize the data. 

The histplot() function produces a histogram. I used the 'price' column for the x axis, resulting in a histogram that groups the 201 automobiles by price.  

```
sns.histplot(data=df, x='price')
```
![Price Histogram]({{ site.baseurl }}/assets/images/2024-02-18-Python-Data-Visualization/price-histogram.webp)
