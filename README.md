# Retail-Pricing-optimization-Analysis
This project was conducted in response to a management request to investigate the decline in profit margins across the Haven Coffee Sales portfolio. The primary concern was the rising Cost of Goods Sold (COGS), tariffs, and other cost factors affecting overall profitability.

Using order data from 2023 to 2025, this analysis evaluates gross margin performance and provides data-driven recommendations to improve pricing strategy.

## 📧 Business Problem

Management observed a significant decline in profit margins and requested:

Identification of products with Gross Margin Percentage (GMP) below 30% in Q3 2025
A comprehensive dashboard showing:

Year-over-Year Gross Margin Percentage trends

Revenue by Category

Revenue by Product

Revenue by Region

## 🎯 Objectives
Identify low-performing products based on profitability

Analyze trends in Gross Margin Percentage over time

Evaluate revenue distribution across categories, products, and regions

Provide actionable recommendations to improve pricing strategy

## 🛠️ Tools & Technologies

SQL Server – Data cleaning, transformation, and analysis

Excel – Data validation

Power BI – Dashboard development and visualization

##🔍 SQL Analysis

```
--combining the year order tables
WITH all_order AS(
SELECT 
OrderID,
CustomerID,
ProductID,
OrderDate,
Quantity,
Revenue,
COGS
FROM Orders_2023

UNION ALL

SELECT 
OrderID,
CustomerID,
ProductID,
OrderDate,
Quantity,
Revenue,
COGS
FROM Orders_2024

UNION ALL

SELECT 
OrderID,
CustomerID,
ProductID,
OrderDate,
Quantity,
Revenue,
COGS
FROM Orders_2025)
--- building the main dataset query
SELECT
a.OrderID,
a.CustomerID,
c.Region,
a.OrderDate,
DATEPART(WEEK,a.OrderDate) as week_number,
DATEPART(YEAR,a.OrderDate) as years,
c.CustomerJoinDate,
a.Quantity,
a.Revenue,
CASE when a.Revenue is null then p.price*a.Quantity else a.Revenue END Cleaned_Revenue,
a.Revenue - a.COGS as profit,
a.COGS,
p.ProductName,
p.ProductCategory,
p.Price,
p.Base_Cost
FROM all_order a
left join customers c
on a.CustomerID = c.CustomerID
left join products p
on a.ProductID = p.ProductID
where a.CustomerID is not null --- drop non customerID

```

 Data Preparation
 
Handled NULL values

Created calculated fields 

Aggregated data by Year, Product, Category, and Region


## 📊 Dashboard Features


The Power BI dashboard includes:

 Year-over-Year GMP Trend
 
 Revenue by Category
 
 Revenue by Product
 
 Revenue by Region
 
 Highlight of Low Margin Products (<30%)


## 💡 Key Insights
Several products in Q3 2025 recorded GMP below 30%, indicating profitability issues

Rising COGS significantly impacted margins across multiple categories

Some high-revenue products generated low profit margins, reducing overall profitability

Regional differences suggest pricing inconsistencies or cost variations

## PRICING RECOMMENDATIONS

Based on the analysis of Gross Margin Percentage (GMP), some products are not making enough profit. Below are the key actions to take:

# 1. Review Low-Margin Products

The following products have very low profit margins and need urgent attention:

Chemex Filters (100 pack) – 14.58%

Minutoist Keychain – 15.59%

Logo Hoodie (Black) – 16.34%

For these products, the company should either:

Stop selling them (discontinue), or

Increase their prices by at least 25% to improve profitability

# 2. Adjust Pricing for Key Product

The Gooseneck Electric Kettle should have its price increased so that its Gross Margin Percentage goes above 30%.

# 3. Why This Matters
The cost of goods sold (COGS) has been increasing, which is reducing profit margins.
If no action is taken, these products will continue to bring low returns and affect overall business performance.

# 4. Expected Outcome
By increasing prices or removing weak products, the company can:

Improve overall profit margins
Focus on more profitable products
Build a stronger and more sustainable pricing strategy

