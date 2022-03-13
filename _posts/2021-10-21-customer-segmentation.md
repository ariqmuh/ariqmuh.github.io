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

<p>Attribute Information:<p/>
   <table>
  <tr>
    <th>Attribute</th>
    <th>Data Type</th>
    <th>Description</th>
    <th>Unit Analysis</th>
  </tr>
  <tr>
    <td>order_id</td>
    <td>object</td>
    <td>Unik ID dari order</td>
    <td>Setiap baris merepresentasikan ID order yang yang muncul ketika customer
    melakukan order</td>
  </tr>
  <tr>
    <td>order_purchase_stamp</td>
    <td>datetime64[s]</td>
    <td>Waktu pembelian customer</td>
    <td>Setiap baris merepresentasikan waktu ketika customer melakukan order</td>
  </tr>
  <tr>
    <td>order_item_id</td>
    <td>float64</td>
    <td>Jumlah barang per-order</td>
    <td>Setiap baris merepresentasikan jumlah barang yang dibeli customer dalam sekali order</td>
  </tr>
  <tr>
    <td>product_id</td>
    <td>object</td>
    <td>ID dari sebuah product</td>
    <td>Setiap baris merepresentasikan ID dari sebuah product yang diorder oleh customer</td>
  </tr>
  <tr>
    <td>price</td>
    <td>float64</td>
    <td>Harga dari sebuah product</td>
    <td>Setiap baris merepresentasikan harga dari sebuah product yang diorder oleh customer</td>
  </tr>
  <tr>
    <td>payment_sequential</td>
    <td>float64</td>
    <td>Jumlah payment method</td>
    <td>Setiap baris merepresentasikan jumlah metode payment yang dilakukan oleh customer. Customer dapat membayar sebuah transaksi lebih dari 1 metode</td>
  </tr>
  <tr>
    <td>payment_type</td>
    <td>object</td>
    <td>Metode pembayaran</td>
    <td>Setiap baris merepresentasikan metode yang digunakan customer dalam membayar sebuah transaksi</td>
  </tr>
  <tr>
    <td>payment_value</td>
    <td>float64</td>
    <td>Nilai Transaksi</td>
    <td>Setiap baris merepresentasikan nilai transaksi yang harus dibayar customer</td>
  </tr>
  <tr>
    <td>review_score</td>
    <td>float64</td>
    <td>Tingkat kepuasan customer</td>
    <td>Setiap baris merepresentasikan tingkat kepuasan customer dalam bertransaksi, nilainya dari 1 - 5</td>
  </tr>
  <tr>
    <td>customer_unique_id</td>
    <td>object</td>
    <td>Unik ID dari customer</td>
    <td>Setiap baris merepresentasikan ID customer yang melakukan
    order</td>
  </tr>
  <tr>
    <td>product_category_name_english</td>
    <td>object</td>
    <td>Kategori product</td>
    <td>Setiap baris merepresentasikan nama kategori dari sebuah product dalam Bahasa Inggris</td>
  </tr>
  <tr>
    <td>month_order</td>
    <td>object</td>
    <td>Nama bulan order dilakukan</td>
    <td>Setiap baris merepresentasikan nama bulan dari tanggal pembelian dilakukan</td>
  </tr>
  <tr>
    <td>weekday_order</td>
    <td>object</td>
    <td>Nama hari order dilakukan</td>
    <td>Setiap baris merepresentasikan nama hari dari tanggal pembelian dilakukan</td>
  </tr>
  <tr>
    <td>month_year_order</td>
    <td>period[M]</td>
    <td>Tahun dan bulan pembelian</td>
    <td>Setiap baris merepresentasikan tahun dan bulan dari tanggal pembelian dilakukan</td>
  </tr>
</table>

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
