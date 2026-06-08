# ===============================
# RETAIL SALES ANALYSIS PROJECT
# POWER BI READY FULL CODE
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
    "discount": np.round(np.random.uniform(0, 0.3, n), 2)
}

df = pd.DataFrame(data)

# ===============================
# 2. FEATURE ENGINEERING
# ===============================

df["sales"] = df["quantity"] * df["price"] * (1 - df["discount"])

df["profit"] = df["sales"] * 0.25  # assumed margin

df["date"] = pd.to_datetime(df["date"])

df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["month_name"] = df["date"].dt.strftime("%B")
df["day"] = df["date"].dt.day
df["weekday"] = df["date"].dt.day_name()

df["revenue_per_unit"] = df["price"] * (1 - df["discount"])

# ===============================
# 3. SAVE DATASET (POWER BI INPUT)
# ===============================

df.to_csv("sales_data.csv", index=False)
df.to_excel("sales_data.xlsx", index=False)

print("Dataset created and saved successfully (CSV + Excel)")

# ===============================
# 4. LOAD DATA (SIMULATE POWER BI INPUT CHECK)
# ===============================

df = pd.read_csv("sales_data.csv")
df["date"] = pd.to_datetime(df["date"])

print("\nDATA OVERVIEW")
print(df.head())

print("\nINFO")
print(df.info())

print("\nMISSING VALUES")
print(df.isnull().sum())

# ===============================
# 5. BASIC ANALYSIS
# ===============================

total_sales = df["sales"].sum()
total_profit = df["profit"].sum()

print("\nTOTAL SALES:", total_sales)
print("TOTAL PROFIT:", total_profit)

# ===============================
# 6. MONTHLY SALES TREND
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
# 7. TOP PRODUCTS
# ===============================

top_products = df.groupby("product")["sales"].sum().sort_values(ascending=False)

plt.figure(figsize=(8,5))
sns.barplot(x=top_products.index, y=top_products.values)
plt.title("Top Products by Sales")
plt.show()

# ===============================
# 8. REGION ANALYSIS
# ===============================

region_sales = df.groupby("region")["sales"].sum()

plt.figure(figsize=(6,6))
plt.pie(region_sales, labels=region_sales.index, autopct="%1.1f%%")
plt.title("Sales by Region")
plt.show()

# ===============================
# 9. CATEGORY ANALYSIS
# ===============================

category_sales = df.groupby("category")["sales"].sum()

plt.figure(figsize=(6,4))
sns.barplot(x=category_sales.index, y=category_sales.values)
plt.title("Category Sales")
plt.show()

# ===============================
# 10. BEST DAYS
# ===============================

best_days = df.groupby("date")["sales"].sum().sort_values(ascending=False).head(10)

print("\nTOP 10 SALES DAYS")
print(best_days)

# ===============================
# 11. TOP ORDERS
# ===============================

top_orders = df.groupby("order_id")["sales"].sum().sort_values(ascending=False).head(10)

print("\nTOP 10 ORDERS")
print(top_orders)

# ===============================
# 12. FINAL BUSINESS INSIGHTS
# ===============================

print("\n====================")
print("BUSINESS INSIGHTS")
print("====================")

print("Total Sales:", total_sales)
print("Total Profit:", total_profit)
print("Best Product:", top_products.idxmax())
print("Best Region:", region_sales.idxmax())
print("Best Category:", category_sales.idxmax())

print("\nAnalysis Completed Successfully 🚀")

# ===============================
# 13. POWER BI READY EXPORT FILE
# ===============================

# Final clean dataset for Power BI
powerbi_df = df[[
    "order_id", "date", "year", "month", "month_name", "weekday",
    "region", "product", "category",
    "quantity", "price", "discount",
    "sales", "profit"
]]

powerbi_df.to_csv("POWERBI_SALES_DATA.csv", index=False)

print("\nPOWER BI FILE CREATED: POWERBI_SALES_DATA.csv")
