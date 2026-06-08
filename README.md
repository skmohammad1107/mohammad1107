# Data Analytics Portfolio

## About Me

I am a Data Analyst passionate about transforming raw data into actionable business insights. My expertise includes SQL, Python, Power BI, Excel, Data Visualization, Statistical Analysis, and Machine Learning.

### Skills

- SQL
- Python
- Pandas
- NumPy
- Power BI
- Tableau
- Excel
- Machine Learning
- Statistics
- Data Visualization

---

# Featured Project: E-Commerce Sales Intelligence Platform

## Business Problem

An e-commerce company wanted to improve revenue, increase customer retention, identify high-performing products, and forecast future sales.

## Project Objectives

- Analyze sales performance
- Understand customer behavior
- Identify profitable products
- Forecast future revenue
- Build an executive dashboard

## Tools Used

- Python
- SQL
- Power BI
- Excel
- Scikit-Learn

## Dataset

- 500,000+ sales transactions
- Customer information
- Product catalog
- Regional sales records

---

## Data Cleaning

### Tasks Performed

- Removed duplicate records
- Handled missing values
- Standardized product categories
- Corrected date formats
- Validated transaction data

### Results

- Eliminated 4,500 duplicate records
- Resolved all missing values
- Improved data quality for analysis

---

## Exploratory Data Analysis

### Sales Analysis

Key Findings:

- Revenue increased by 18% year-over-year.
- Q4 generated the highest sales volume.
- Weekend purchases were significantly higher than weekdays.

### Customer Analysis

Key Findings:

- Top 20% of customers generated 65% of total revenue.
- Returning customers spent 2.3 times more than new customers.

### Product Analysis

Key Findings:

- Electronics generated the highest revenue.
- Several products had strong sales but low profit margins.

---

## SQL Analysis

### Top Revenue-Producing Products

```sql
SELECT Product_Name,
       SUM(Sales) AS Revenue
FROM Sales
GROUP BY Product_Name
ORDER BY Revenue DESC;
