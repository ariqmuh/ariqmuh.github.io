---
title: "Customer Segmentation using RFM and K-Means Clustering"
date: 2021-10-21
tags: [data manipulation, data visualization, data science, clustering]
header:
excerpt: "Data Manipulation, Data Visualization, Data Science, Clustering"
mathjax: "true"
---

# • Project Description 
In this project, I put myself as a part of the Data Scientist Team of Olist, e-commerce in Brazil. I was assigned to help the marketing team create segmentation of Olist customers based on their behavior. The models used in this project are the RFM (Recency, Frequency, & Monetary) Segmentation and K-Means Clustering.   

Full Documentation: [Customer Segmentation using RFM and K-Means Clustering](https://github.com/ariqmuh/Portfolios/tree/main/Customer_Segmentation_using_RFM_and_KMeans_Clustering)   

# • Background 
![E-commerce Users in Brazil]({{ site.url }}{{ site.baseurl }}/images/statistic.JPG)     
    
In today's technological era, the e-commerce business is a common thing that can be found. E-commerce itself is a business model that allows a company or individual to buy or sell their products via the internet. E-commerce users from year to year also increase, especially in Brazil. The following is the data of E-commerce users from 2017 to 2025.  

Revenue from the marketplace business model can come from paid features, advertisements, payment gateways, and partnerships. The point is that the more users or traffic on a marketplace, the more revenue you will get. One way to increase users or traffic on a marketplace is to do a Marketing Campaign, such as giving discounts, copywriting, etc. In general, companies prepare a budget of 5% -12% of the total revenue they get to carry out marketing campaigns. However, the problem is that the marketing campaign that is carried out is not right on target, so the company suffers a loss. A marketing campaign can be successfully measured by how many new users it manages to get and how many old users it retains to keep using the marketplace.  
    
To overcome this, one way that can be done is to segment customers or what is commonly referred to as Customer Segmentation. Customer Segmentation helps marketplace owners to group customers with similar characteristics. By using Customer Segmentation, companies can effectively conduct marketing campaigns so that user transactions and user loyalty can increase. According to a survey conducted by Researchscape and Evergage in 2020, 99% of marketers agree that personalization helps strengthen customer relationships and 78% of those results claim that the impact is powerful.  
    
# • Data Understanding
This data was taken from 2016 to 2018 and publicly distributed on Kaggle in September 2018. The existing data contains customer and seller transactions. To solve this problem, we only need data related to customer transactions because what we want to do is customer segmentation, which is useful for knowing a customer's behavior in a transaction.  

Dataset Source : [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/olistbr/brazilian-ecommerce)     
![Data Scheme]({{ site.url }}{{ site.baseurl }}/images/data_scheme.JPG)  

# • Business Problem :

1. How to segment the customers at Olist marketplace so we can divide customers based on their shopping behaviour?
2. What kind of treatment for each cluster to increase retention rate customer?

# • Workflow:
1. Data Merging
```python
# Import Dataset
olist_order = pd.read_csv(Dataset\olist_orders_dataset.csv')
olist_item = pd.read_csv(Dataset\olist_order_items_dataset.csv')
olist_payment = pd.read_csv(Dataset\olist_order_payments_dataset.csv')
olist_product = pd.read_csv(Dataset\olist_products_dataset.csv')
olist_customer = pd.read_csv(Dataset\olist_customers_dataset.csv')
olist_review = pd.read_csv(Dataset\olist_order_reviews_dataset.csv')
olist_translate = pd.read_csv(Dataset\product_category_name_translation.csv')

# Merge Dataset
df_olist = pd.merge(olist_order, olist_item, on='order_id', how='left')
df_olist = pd.merge(df_olist, olist_product, on='product_id', how='inner')
df_olist = pd.merge(df_olist, olist_payment, on='order_id', how = 'left')
df_olist = pd.merge(df_olist, olist_review, on='order_id', how='left')
df_olist = pd.merge(df_olist, olist_customer, on='customer_id', how='right')
df_olist = pd.merge(df_olist, olist_translate, on='product_category_name', how='inner')
```

2. Data Cleaning and Data Pre-processing
```python
# Drop Unused Columns
df_olist_clean = df_olist.drop(columns=['order_status', 'order_approved_at', 'order_delivered_customer_date', 'order_delivered_carrier_date','order_delivered_customer_date', 'order_estimated_delivery_date', 'seller_id', 'shipping_limit_date','product_category_name', 'product_name_lenght', 'product_description_lenght', 'product_weight_g', 'product_length_cm', 'product_height_cm', 'product_width_cm', 'payment_installments','review_id', 'review_comment_title', 'review_comment_message', 'review_creation_date', 'review_answer_timestamp', 'customer_id', 'customer_city', 'customer_state', 'product_photos_qty', 'freight_value', 'payment_sequential'])

# Drop Missing Values
df_olist_clean.dropna(inplace = True)

# Drop Duplicate Values
df_olist_clean = df_olist_clean.drop_duplicates()

# Handling Inconsistent Variable
def format_val(x):
  if x == 'home_appliances_2':
    return "home_appliances"
  elif x == 'home_confort':
    return "home_comfort"
  elif x == "home_comfort_2":
    return "home_comfort"
  return x
df_olist_clean['product_category_name_english'] = df_olist_clean['product_category_name_english'].apply(format_val)

# Casting Datatype
df_olist_clean['order_purchase_timestamp'] = pd.to_datetime(df_olist_clean['order_purchase_timestamp'])
df_olist_clean['order_purchase_timestamp'].dt.strftime('%Y-%m-%d')

# Create New Columns
df_olist_clean['month_order'] = df_olist_clean['order_purchase_timestamp'].dt.month_name()
df_olist_clean['weekday_order'] = df_olist_clean['order_purchase_timestamp'].dt.day_name()
df_olist_clean['month_year_order'] = df_olist_clean['order_purchase_timestamp'].dt.to_period('M').astype(str)
df_olist_clean['date_order'] = df_olist_clean['order_purchase_timestamp'].dt.day
```

4. Exploratory Data Analysis (EDA)
5. Modeling (K-Means Clustering using RFM)
6. Conclusion
7. Business Recommendation

# • Model
In this section, we use Recency, Frequency, and Monetary from customers. These three things can describe the transaction behavior of a customer. The meaning of RFM itself is:  

- Recency: The last time a customer made a purchase  
- Frequency: Number of transactions  
- Monetary: The spending power of a customer  

This RFM metric is an important indicator of customer behavior segmentation because the frequency and monetary affect customer lifetime value, and recency effect engagement rate.  

The model we tried had two models, namely RFM Segmentation and K-Means Clustering. 

1. RFM Segmentation, we calculate the segmentation score by combining the scores from R, F, and M into a unique combination in the form of a string. For example, if R = 1, F = 1, and M = 1 then the RFM Segmentation Score becomes 1 + 1 + 1 = 111 and from that score we provide segmentation to customers.
2. 




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
