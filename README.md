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
SELECT 
    Country AS customer_country, 
    COUNT(CustomerID) AS number_of_customers
FROM Customers
GROUP BY Country
ORDER BY number_of_customers DESC;
```

Insight

Customers are spread across multiple countries, confirming a global customer base and supporting international expansion opportunities.

### 2. Missing Data Audit

```sql
SELECT 
    CustomerID, 
    CompanyName, 
    ContactName, 
    ContactTitle, 
    Country
FROM Customers
WHERE Region IS NULL
ORDER BY Country, CompanyName;
```

Insight

A portion of customer records have missing region data, which can affect logistics planning and targeted marketing.

### 3. Order Volume Overview

```sql
SELECT 
    COUNT(*) AS total_orders,
    COUNT(DISTINCT CustomerID) AS unique_customers,
    MIN(OrderDate) AS first_order_date,
    MAX(OrderDate) AS last_order_date
FROM Orders;
```

Insight

The total number of orders reflects steady transaction activity and overall business engagement.

### 4. Revenue Calculation

```sql
SELECT 
    SUM(UnitPrice * Quantity * (1 - Discount)) AS total_revenue,
    COUNT(*) AS total_line_items,
    AVG(UnitPrice * Quantity * (1 - Discount)) AS avg_line_value
FROM [Order Details];
```

Insight

The business generates strong revenue, showing consistent commercial performance across orders.

### 5. Product Performance by Category

```sql
SELECT 
    c.CategoryID,
    c.CategoryName,
    COUNT(p.ProductID) AS product_count,
    AVG(p.UnitPrice) AS avg_unit_price
FROM Products p
JOIN Categories c ON p.CategoryID = c.CategoryID
GROUP BY c.CategoryID, c.CategoryName
ORDER BY product_count DESC;
```

Insight

Product distribution varies across categories, highlighting areas with higher product concentration.

### 6. High-Value Customers

```sql
SELECT 
    o.CustomerID,
    c.CompanyName,
    COUNT(DISTINCT o.OrderID) AS order_count,
    SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)) AS total_revenue
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
JOIN [Order Details] od ON o.OrderID = od.OrderID
GROUP BY o.CustomerID, c.CompanyName
HAVING COUNT(DISTINCT o.OrderID) > 10
ORDER BY total_revenue DESC;
```

Insight

A smaller group of customers contributes a large portion of total orders, indicating strong repeat purchasing behavior.

### 7. Average Freight per Customer

```sql
SELECT 
    CustomerID,
    COUNT(OrderID) AS total_orders,
    AVG(Freight) AS avg_freight,
    CASE 
        WHEN AVG(Freight) > 100 THEN 'High Freight'
        WHEN AVG(Freight) > 50 THEN 'Medium Freight'
        ELSE 'Low Freight'
    END AS freight_segment
FROM Orders
GROUP BY CustomerID
ORDER BY avg_freight DESC;
```

Insight

Freight costs vary significantly across customers, suggesting differences in shipping distance or order size.

### 8. Supplier Contribution Analysis

```sql
SELECT Suppliers.SupplierID, 
       Suppliers.ContactName, 
       COUNT(Products.ProductID) AS product_supply_count
FROM Suppliers
INNER JOIN Products ON Suppliers.SupplierID = Products.SupplierID
GROUP BY Suppliers.SupplierID, Suppliers.ContactName
HAVING COUNT(Products.ProductID) >= 5;
```

Insight

Certain suppliers contribute more products, making them critical to supply chain stability.

### 9. Strong Market Identification

```sql
SELECT 
    c.Country,
    COUNT(DISTINCT c.CustomerID) AS customer_count,
    COUNT(DISTINCT o.OrderID) AS total_orders,
    SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)) AS total_revenue
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
LEFT JOIN [Order Details] od ON o.OrderID = od.OrderID
GROUP BY c.Country
HAVING COUNT(DISTINCT c.CustomerID) > 5
ORDER BY total_revenue DESC;
```

Insight

Some countries have higher customer concentration, making them priority markets for growth.

### 10. Pending Shipments

```sql
SELECT Shippers.ShipperID, 
       Shippers.CompanyName, 
       COUNT(Orders.OrderID) AS pending_shipments
FROM Shippers
INNER JOIN Orders ON Shippers.ShipperID = Orders.ShipVia
WHERE Orders.ShippedDate IS NULL
GROUP BY Shippers.ShipperID, Shippers.CompanyName;
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
