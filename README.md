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
sales_by_type = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)
plt.figure(figsize=(10,6))
bars = plt.bar(sales_by_type.index, sales_by_type.values)
plt.xticks(rotation=90)
plt.xlabel('ItemType')
plt.ylabel('Total Sales')
plt.title('Total Sales By Item Type')
for bar in bars:
    plt.text(bar.get_x()+bar.get_width()/2,bar.get_height(),
             f'{bar.get_height():,.0f}',ha='center',va = 'bottom',fontsize = 8)
    plt.tight_layout()
    plt.show()       
    grouped = df.groupby(['Outlet Location Type','Item Fat Content'])['Sales'].sum().unstack()
grouped = grouped[['Regular','Low Fat']]
ax = grouped.plot(kind = 'bar',figsize = (8,5), title = 'Outlet Tier by Item Fat Content')
plt.xlabel('Outlet Location Tier')
plt.ylabel('Total Sales')
plt.legend(title='Total Fat Content')
plt.tight_layout()
plt.show()
sales_by_year = df.groupby('Outlet Establishment Year')['Sales'].sum().sort_index()
plt.figure(figsize=(9,5))
plt.plot(sales_by_year.index,sales_by_year.values, marker = 'o', linestyle ='-')
plt.xlabel('Outlet Establishment Year')
plt.ylabel('Total Sales')
plt.title('Outlet Establishment')
for x,y in zip(sales_by_year.index,sales_by_year.values):
    plt.text(x,y,
             f'{y:,.0f}',ha='center',va = 'bottom',fontsize = 8)
plt.tight_layout()
plt.show()
Sales_by_size = df.groupby('Outlet Size')['Sales'].sum()
plt.figure(figsize=(4,4))
plt.pie(Sales_by_size, labels = Sales_by_size.index,
        autopct='%.1f%%',
        startangle = 90)
plt.title('Outlet Size')
plt.axis('equal')
plt.show()
sales_by_Location = df.groupby('Outlet Location Type')['Sales'].sum().reset_index()
sales_by_Location = sales_by_Location.sort_values('Sales',ascending=False)

plt.figure(figsize=(8,3))
ax = sns.barplot(x='Sales',y='Outlet Location Type',data= sales_by_Location)

plt.title('Total Sales By Outlet Location Type')
plt.xlabel('Total Sales')
plt.ylabel('Outlet Location Type')

plt.tight_layout()
plt.show()

