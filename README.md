# RFM-analysis-

**RFM Analysis Using Python.**

RFM stands for recency, frequency, monetary value. In business analytics, we often use this concept to divide customers into different segments, like high-value customers, medium value customers or low-value customers, and similarly many others.
Recency: How recently has the customer made a transaction with us.
Frequency: How frequent is the customer in ordering/buying some product from us.
Monetary: How much does the customer spend on purchasing products from us.
Recency, Frequency, and Monetary value of a customer are three key metrics that provide information about customer engagement, loyalty, and value to a business.

Let’s assume we are a company, our company name is Neos Gen Investment, let’s perform the RFM analysis on our customers.

```python
#performing the analysis
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
df = pd.read_csv (r"C:\Users\LGICHERU1\Desktop\rfm_data.csv")
print (df)
from datetime import datetime
#Calculating the RFM values
df['PurchaseDate'] = pd.to_datetime(df['PurchaseDate'])
todays_date = datetime(2023,10,16) #todays date
print (df['PurchaseDate'])
#Recency
df ['recency'] = (todays_date - df['PurchaseDate']).dt.days
#Frequency
frequency = df.groupby('CustomerID')['PurchaseDate'].count().reset_index()
frequency.rename(columns={'PurchaseDate':'frequency'}, inplace=True)
#Monetary
monetary = df.groupby('CustomerID')['TransactionAmount'].sum().reset_index()
monetary.rename(columns={'TransactionAmount':'monetary'}, inplace=True)
print (monetary)
#combining the three
rfm = pd.merge(frequency, monetary, on='CustomerID')
rfm2 = pd.merge( rfm, df [['recency','CustomerID']], on ='CustomerID')
print (rfm2)
#visualizing the RFM
# Creating histogram
plt.figure(figsize=(10, 10))
plt.subplot(221)
plt.hist(rfm2['recency'], bins=50, edgecolor='brown', alpha=0.9, color='green')
plt.xlabel('recency')
plt.title('Nes Gen Recency')
plt.subplot(222)
plt.hist(rfm2['frequency'], bins=20, edgecolor='yellow', alpha=0.5, color='blue')
plt.xlabel('frequency')
plt.title('Neos Gen Frequency')
plt.subplot(223)
plt.hist(rfm2['monetary'], bins=50, edgecolor='red', alpha=0.9, color='black')
plt.xlabel('monetary')
plt.title('Neos Gen  Monetary')
plt.show()
```

**Summary**

RFM Analysis is used to understand and segment customers based on their buying behaviour. RFM stands for recency, frequency, and monetary value, which are three key metrics that provide information about customer engagement, loyalty, and value to a business. I hope you liked this article on RFM Analysis using Python. 

**You can download the data from the link provided and execute this code** (https://statso.io/rfm-analysis-case-study/)
