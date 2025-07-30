#WEB SCRAPING from FLIPKART ON TOPIC- Mobile phones under 50,000(as done during web scraping)
import requests
from bs4 import BeautifulSoup
for i in range(1, 11):
    url = "https://www.flipkart.com/search?q=mobile+phones+under+50000&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as=off&page=" + str(i)
    r = requests.get(url)
    print(r)
    print(url)
import pandas as pd 
import requests
from bs4 import BeautifulSoup
url = "https://www.flipkart.com/search?q=mobile+phones+under+50000&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as=off&page=1"
product_name=[]
prices=[]
description=[]
reviews=[]
r= requests.get(url)
#nt(r)
soup = BeautifulSoup(r.text,"lxml")
box=soup.find("div",class_="DOjaWF gdgoEp")
names = box.find_all("div",class_="KzDlHZ")
print(names)                      
import pandas as pd 
import requests
from bs4 import BeautifulSoup

url = "https://www.flipkart.com/search?q=mobile+phones+under+50000&page=1"
product_name = []
prices = []
description = []
reviews = []

r = requests.get(url)
soup = BeautifulSoup(r.text, "lxml")
names = box.find_all("div", class_="KzDlHZ")

for i in names:
    name = i.text.strip()
    product_name.append(name)
print("PRODUCT NAME:",product_name)
prices = box.find_all("div", class_="Nx9bqj _4b5DiR")
price_list = []  
for i in prices:
    name = i.text.strip()
    price_list.append(name)
print("LIST OF PRODUCT PRICE:",price_list)
desc = box.find_all("ul",class_="G4BRas")
for i in desc:
    name=i.text
    description.append(name)
    print("PRODUCT DESCRIPTION:",description)
reviews = box.find_all("div", class_="XQDdHH")
review_list = []
for i in reviews:
    name = i.text.strip()
    review_list.append(name)
print("LIST OF REVIEWS:",review_list)
for i in range(2,13):
    df=pd.DataFrame({"PRODUCTS":product_name,"PRICES":price_list,"DESCRIPTION":description ,"REVIEW":review_list})
print(df)

import seaborn as sns
import matplotlib.pyplot as plt

#PRICE DISTRIBUTION
sns.histplot(df["PRICES"], kde=True, bins=15)
plt.title("Price Distribution of Mobiles Under ₹50,000")
plt.xlabel("Price (INR)")
plt.ylabel("Count")
plt.show()
#LIST OF TOP 10 MOST EXPENSIVE PHONES
df.sort_values(by="PRICES", ascending=False).head(10)

#DATA VISUALIZING TOP 10 MOST EXPENSIVE PHONES
top10 = df.sort_values(by="PRICES", ascending=False).head(10)
plt.figure(figsize=(10, 6))
sns.barplot(x="PRICES", y="PRODUCTS", data=top10, palette="viridis",hue="PRODUCTS")
plt.title("Top 10 Most Expensive Mobiles under ₹50,000 on Flipkart")
plt.xlabel("Price (₹)")
plt.ylabel("Product Name")
plt.show()

#DATA VISUALISING OF DESCENDING WORD COUNT
df["Desc_Word_Count"] = df["DESCRIPTION"].apply(lambda x: len(x.split()))
sns.scatterplot(data=df, x="Desc_Word_Count", y="PRICES")
plt.title("Price vs Description Length")
plt.xlabel("Description Word Count")
plt.ylabel("Price (₹)")
plt.show()
#LIST OF TOP REVIEWED PRODUCTS
df["Review_Length"] = df["REVIEW"].apply(lambda x: len(x.split()))
top_reviews = df.sort_values(by="Review_Length", ascending=False).head(10)
top_reviews[["PRODUCTS", "REVIEW"]]

#DATA VISUALISATION OF TOP 10 MOBILES WITH MOST REVIEWS ON FLIPKART
plt.figure(figsize=(12, 6))
sns.barplot(
    y="PRODUCTS", 
    x="Review_Length", 
    data=top_reviews)
plt.title("Top 10 Mobiles with Most Reviews on Flipkart")
plt.xlabel("Review Length (Word Count)")
plt.ylabel("Product Name")
plt.tight_layout()
plt.grid(axis='x')
plt.show()
#BOXPLOT DATA VISUALISATION OF OUTLIERS IN PRICE
sns.boxplot(x=df["PRICES"])
plt.title("Price Outliers in Mobile Phones")
plt.show()

#PRICE RANGE
print("Min Price:", df["PRICES"].min())
print("Max Price:", df["PRICES"].max())
print("Mean Price:", df["PRICES"].mean())
print("Median Price:", df["PRICES"].median())

#PRODUCT WITH LOWEST AND HIGHEST PRICE AND NO. OF REVIEWS
lowest_price = df.sort_values(by="PRICES", ascending=True).head(1)
print("Lowest Priced Product:")
print(lowest_price[["PRODUCTS", "PRICES", "REVIEW"]])
highest_price = df.sort_values(by="PRICES", ascending=False).head(1)
print("\nHighest Priced Product:")
print(highest_price[["PRODUCTS", "PRICES", "REVIEW"]])
