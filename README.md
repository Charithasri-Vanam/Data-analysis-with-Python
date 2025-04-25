# Data-analysis-with-Python
This project focuses on conducting data quality validation and exploratory data analysis (EDA) on a real-world grocery dataset from Blinkit (a fast delivery retail platform). It demonstrates how to assess the health and reliability of sales data before deriving insights, which is crucial for making informed business decisions.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
df=pd.read_excel("C:/Users/chari/Downloads/BlinkIT Grocery Data.xlsx")
df.head(10)
df.tail(10)
df.shape
df.columns
df.dtypes
print(df['Item Fat Content'].unique())
print(df['Item Identifier'].unique())
df['Item Fat Content'] = df['Item Fat Content'].replace({'LF':'Low Fat', 'reg':'Regular','low fat':'Low Fat'})
print(df['Item Fat Content'].unique())
total_sales = df['Sales'].sum()
print(total_sales)
avg_sales = df['Sales'].mean()
no_of_items_sold = df['Sales'].count()
avg_rating = df['Rating'].mean()
print(f"Total Sales: ${total_sales:,.0f}")
print(f"Average Sales: ${avg_sales:,.0f}")
print(f"No of Items Sold: ${no_of_items_sold:,.0f}")
print(f"Average Rating: ${avg_rating:,.1f}")
Sales_by_fat = df.groupby('Item Fat Content')['Sales'].sum()
plt.pie(Sales_by_fat, labels = Sales_by_fat.index,
        autopct='%.2f%%',
        startangle = 90)
plt.title('sales by fat content')
plt.axis('equal')
plt.show()
                          
