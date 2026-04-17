# Northwind SQL & Excel Business Analysis

Customer Behavior, Revenue Performance, and Operational Insights

## Overview

This project analyzes the Northwind retail database using SQL and Excel to solve real business problems.

The focus is simple.
Move from raw data to clear decisions.

I used SQL to extract structured insights, then Excel to visualize and communicate those insights in a way business teams can understand and act on.

This project reflects how a data analyst works in real scenarios.

## Problem Statement

Businesses collect large volumes of transactional data, but most struggle to turn that data into clear insights.

Key questions often remain unanswered:

Where are our customers located
Who are our most valuable customers
How much revenue are we generating
Which markets are strongest
Where are operational delays happening

This project answers these questions using SQL queries and Excel-based reporting.

## Project Objectives

Understand customer distribution across countries
Evaluate total business activity and revenue performance
Identify high-value and repeat customers
Detect missing or incomplete data
Analyze supplier and product distribution
Track operational inefficiencies such as pending shipments
Present findings clearly using Excel visualizations

## Dataset Description

Source: Northwind Database (SQLite)

Tables used:

Customers
Customer details including country and region

Orders
Transaction-level order data

Order Details
Product-level breakdown of each order

Products
Product catalog and category linkage

Suppliers
Supplier information

Categories
Product grouping structure

## Tools Used

SQL (SQLite) for querying
SQLite Online for execution
Microsoft Excel for analysis and visualization
GitHub for project documentation

## Project Workflow

Loaded dataset into SQLite environment
Explored table structure and relationships
Wrote SQL queries to answer business questions
Validated outputs for accuracy
Exported results into Excel
Built visualizations for each analysis
Interpreted insights for business use

## Business Questions and Analysis

### 1. Customer Diversity Analysis

```sql
SELECT DISTINCT Country AS customer_country
FROM Customers;
```

Insight

Customers are spread across multiple countries, confirming a global customer base and supporting international expansion opportunities.

### 2. Missing Data Audit

```sql
SELECT CustomerID, CompanyName, Country
FROM Customers
WHERE Region IS NULL;
```

Insight

A portion of customer records have missing region data, which can affect logistics planning and targeted marketing.

### 3. Order Volume Overview

```sql
SELECT COUNT(OrderID) AS total_orders
FROM Orders;
```

Insight

The total number of orders reflects steady transaction activity and overall business engagement.

### 4. Revenue Calculation

```sql
SELECT SUM(UnitPrice * Quantity * (1 - Discount)) AS total_revenue
FROM "Order Details";
```

Insight

The business generates strong revenue, showing consistent commercial performance across orders.

### 5. Product Performance by Category

```sql
SELECT CategoryID, COUNT(ProductID) AS product_count
FROM Products
GROUP BY CategoryID;
```

Insight

Product distribution varies across categories, highlighting areas with higher product concentration.

### 6. High-Value Customers

```sql
SELECT CustomerID, COUNT(OrderID) AS order_count
FROM Orders
GROUP BY CustomerID
HAVING COUNT(OrderID) > 10;
```

Insight

A smaller group of customers contributes a large portion of total orders, indicating strong repeat purchasing behavior.

### 7. Average Freight per Customer

```sql
SELECT CustomerID, AVG(Freight) AS avg_freight
FROM Orders
GROUP BY CustomerID;
```

Insight

Freight costs vary significantly across customers, suggesting differences in shipping distance or order size.

### 8. Supplier Contribution Analysis

```sql
SELECT SupplierID, COUNT(ProductID) AS product_supply_count
FROM Products
GROUP BY SupplierID
HAVING COUNT(ProductID) > 5;
```

Insight

Certain suppliers contribute more products, making them critical to supply chain stability.

### 9. Strong Market Identification

```sql
SELECT Country, COUNT(CustomerID) AS customer_count
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

Insight

Some countries have higher customer concentration, making them priority markets for growth.

### 10. Pending Shipments

```sql
SELECT COUNT(OrderID) AS pending_shipments
FROM Orders
WHERE ShippedDate IS NULL;
```

Insight

Pending shipments highlight operational delays that require attention to improve fulfillment efficiency.

## Excel Visualization

Each SQL output was exported to Excel and structured into:

Raw_Data sheet containing query results
Charts sheet containing visualizations

Charts used:

Bar charts for comparisons
Column charts for totals
KPI style visuals for single metrics

Each chart includes clear titles and short insights to support decision making.

## Key Insights

The business operates across multiple countries, confirming a global footprint

Revenue generation is strong and consistent

A small group of repeat customers drives a significant share of activity

Some customer records contain missing data, affecting accuracy

Top markets are concentrated in a few countries

Operational gaps exist in order fulfillment

Supplier contributions vary, impacting supply chain structure

## Recommendations

Improve data quality by enforcing required fields like region

Focus retention strategies on high-value customers

Invest more in high-performing countries

Optimize logistics to reduce pending shipments

Evaluate supplier relationships for better efficiency

## Project Structure

Northwind-SQL-Excel-Analysis

README.md

sql
queries.sql

excel_outputs
Q1 to Q10 Excel files

images
charts and screenshots

## Learning Outcomes

Applied SQL to solve business problems

Improved ability to structure and query relational data

Learned to translate data into business insights

Developed Excel reporting and visualization skills

Built a portfolio-ready data project

## Future Improvements

Add time-based trend analysis

Build dashboards using Power BI

Introduce advanced SQL techniques like window functions

Expand analysis to product profitability

## Author

Emmanuel Olawumi

Data Analyst
SQL | Excel | Data Analytics
