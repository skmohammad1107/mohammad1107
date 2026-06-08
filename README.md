# ===============================
# RETAIL SALES ANALYSIS PROJECT
# FULL END-TO-END CODE
# ===============================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime, timedelta

# ===============================
# 1. CREATE SYNTHETIC DATASET
# ===============================

np.random.seed(42)

n = 1000
start_date = datetime(2024, 1, 1)

data = {
    "order_id": range(1, n + 1),
    "date": [start_date + timedelta(days=np.random.randint(0, 365)) for _ in range(n)],
    "region": np.random.choice(["North", "South", "East", "West"], n),
    "product": np.random.choice(["Laptop", "Phone", "Tablet", "Headphones"], n),
    "category": np.random.choice(["Electronics", "Accessories"], n),
    "quantity": np.random.randint(1, 5, n),
    "price": np.random.randint(100, 2000, n),
    "discount": np.random.uniform(0, 0.3, n)
}

df = pd.DataFrame(data)

# Sales calculation
df["sales"] = df["quantity"] * df["price"] * (1 - df["discount"])

# Save dataset
df.to_csv("sales_data.csv", index=False)

print("\nDataset created successfully!\n")

# ===============================
# 2. LOAD DATA
# ===============================

df = pd.read_csv("sales_data.csv")

print("\nFirst 5 rows:\n", df.head())
print("\nInfo:\n")
print(df.info())

print("\nMissing values:\n", df.isnull().sum())

# ===============================
# 3. DATA CLEANING
# ===============================

df = df.drop_duplicates()

df["date"] = pd.to_datetime(df["date"])

df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day

print("\nData cleaned successfully!\n")

# ===============================
# 4. BASIC ANALYSIS
# ===============================

print("\nSummary Statistics:\n")
print(df.describe())

# Total sales
total_sales = df["sales"].sum()
print("\nTotal Sales:", total_sales)

# ===============================
# 5. MONTHLY SALES TREND
# ===============================

monthly_sales = df.groupby("month")["sales"].sum()

plt.figure(figsize=(10,5))
sns.lineplot(x=monthly_sales.index, y=monthly_sales.values, marker="o")
plt.title("Monthly Sales Trend")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.grid()
plt.show()

# ===============================
# 6. TOP PRODUCTS
# ===============================

top_products = df.groupby("product")["sales"].sum().sort_values(ascending=False)

plt.figure(figsize=(8,5))
sns.barplot(x=top_products.index, y=top_products.values)
plt.title("Top Products by Sales")
plt.xlabel("Product")
plt.ylabel("Sales")
plt.show()

print("\nTop Products:\n", top_products)

# ===============================
# 7. REGION ANALYSIS
# ===============================

region_sales = df.groupby("region")["sales"].sum()

plt.figure(figsize=(6,6))
plt.pie(region_sales, labels=region_sales.index, autopct="%1.1f%%")
plt.title("Sales by Region")
plt.show()

print("\nRegion Sales:\n", region_sales)

# ===============================
# 8. CATEGORY ANALYSIS
# ===============================

category_sales = df.groupby("category")["sales"].sum()

plt.figure(figsize=(6,4))
sns.barplot(x=category_sales.index, y=category_sales.values)
plt.title("Category Sales")
plt.show()

# ===============================
# 9. PROFIT ESTIMATION
# ===============================

df["profit"] = df["sales"] * 0.25  # assume 25% margin

total_profit = df["profit"].sum()

print("\nTotal Profit:", total_profit)

# ===============================
# 10. BEST DAYS
# ===============================

best_days = df.groupby("date")["sales"].sum().sort_values(ascending=False).head(10)

print("\nTop 10 Sales Days:\n")
print(best_days)

# ===============================
# 11. HIGH VALUE ORDERS
# ===============================

top_orders = df.groupby("order_id")["sales"].sum().sort_values(ascending=False).head(10)

print("\nTop 10 Orders:\n")
print(top_orders)

# ===============================
# 12. FINAL INSIGHTS
# ===============================

print("\n====================")
print("BUSINESS INSIGHTS")
print("====================")

print("1. Total Sales:", total_sales)
print("2. Total Profit:", total_profit)
print("3. Best Selling Product:", top_products.idxmax())
print("4. Best Region:", region_sales.idxmax())
print("5. Best Category:", category_sales.idxmax())

print("\nAnalysis Completed Successfully 🚀")
