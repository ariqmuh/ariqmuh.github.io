---
title: "Customer Segmentation based on Customer Behaviour"
date: 2021-10-21
tags: [data manipulation, data visualization, data science, clustering]
header:
excerpt: "Data Manipulation, Data Visualization, Data Science, Clustering"
mathjax: "true"
---


## 1. Project Description 
<p>This project uses e-commerce transaction data taken from Kaggle. This project aims to analyze customer segmentation based on customer transaction behaviou. The models used in this project are the RFM (Recency, Frequency, & Monetary) model, K-Means Clustering, and Gaussian Clustering.</p>
<p>Full Documentation: <a href="https://github.com/ariqmuh/DataWarrior_JC_DS_VL_01_FinalProject/">Click Here</a><p/>
<p><img src="https://github.com/ariqmuh/ariqmuh.github.io/blob/master/images/Olist.png"><p/>


## 2. Background 
<p><img src="https://github.com/ariqmuh/ariqmuh.github.io/blob/master/images/e-commerce%20user%20in%20brazil%20(1).png" alt="E-commerce Users in Brazil"></p>
<p>In today's technological era, the e-commerce business is a common thing that can be found. *E-commerce* itself is a business model that allows a company or individual to buy or sell their products via the internet. E-commerce users from year to year also increase, especially in Brazil. The following is the data of E-commerce users from 2017 to 2025.</p>

<p>Revenue from the marketplace business model can come from paid features, advertisements, payment gateways, and partnerships. The point is that the more users or traffic on a marketplace, the more revenue you will get. One way to increase users or traffic on a marketplace is to do a Marketing Campaign, such as giving discounts, copywriting, etc. In general, companies prepare a budget of 5% -12% of the total revenue they get to carry out marketing campaigns. However, the problem is that the marketing campaign that is carried out is not right on target, so the company suffers a loss. A marketing campaign can be successfully measured by how many new users it manages to get and how many old users it retains to keep using the marketplace.</p>

<p>To overcome this, one way that can be done is to segment customers or what is commonly referred to as Customer Segmentation. Customer Segmentation helps marketplace owners to group customers with similar characteristics. By using Customer Segmentation, companies can effectively conduct marketing campaigns so that user transactions and user loyalty can increase. According to a survey conducted by Researchscape and Evergage in 2020, 99% of marketers agree that personalization helps strengthen customer relationships and 78% of those results claim that the impact is powerful.</p>

## 3. Data Understanding
<p>This data was taken from 2016 to 2018 and publicly distributed on Kaggle in September 2018. The existing data contains customer and seller transactions. To solve this problem, we only need data related to customer transactions because what we want to do is customer segmentation, which is useful for knowing a customer's behavior in a transaction.</p>

<p><img src="https://i.imgur.com/HRhd2Y0.png" alt="Data Scheme"><p/>



Here's some **bold** text.

What about a [link](https://github.com/dataoptimal)?

Here's a bulleted list:
* First item
+ Second item
- Third item

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
    import numpy as np

    def test_function(x, y):
      z = np.sum(x,y)
      return z
```

R code block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```

Here's some inline code `x+y`.

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg" alt="linearly separable data">

Here's another image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg)

Here's some math:

$$z=x+y$$

You can also put it inline $$z=x+y$$
