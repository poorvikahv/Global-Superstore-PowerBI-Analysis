# Global Superstore – Business Analytics Dashboard

## 1. Project Overview

This project focuses on analyzing Global Superstore retail transaction data using Microsoft Power BI. The objective is to transform raw sales data into meaningful business insights through data cleaning, data modeling, DAX calculations, and interactive visualizations.

The dashboard provides insights into sales performance, profitability, customer segments, product categories, regional performance, shipping operations, and returned orders.

## 2. Problem Statement

Retail businesses generate large amounts of transactional data. However, raw data does not directly provide meaningful information about business performance.

This project addresses the challenge of analyzing sales and operational data to identify profitable products, understand customer purchasing behavior, evaluate regional performance, and identify areas requiring business improvement.

## 3. Project Objectives

- Analyze total sales, total profit, and order performance.
- Identify high-performing and low-performing product categories.
- Evaluate customer segment performance.
- Compare sales and profitability across regions and markets.
- Analyze the relationship between discounts and profitability.
- Evaluate shipping performance and delivery duration.
- Analyze returned orders and return rates.
- Develop an interactive dashboard to support data-driven decision-making.

## 4. Dataset Description

**Dataset Name:** Global Superstore

**Source File:** Global Superstore.xls

**Worksheets Used:**
- Orders – Sales transactions and product details.
- Returns – Returned order information.
- People – Regional manager information.

**Dataset Statistics:**
- Orders: 51,290 transaction rows.
- Returns: 1,173 records.
- People: 13 regional manager records.
- Analysis Period: 2011–2014.
- Distinct Orders: 25,035.
- Distinct Customers: 1,590.

## 5. Tools and Technologies

- Microsoft Power BI Desktop
- Power Query
- DAX (Data Analysis Expressions)
- Microsoft Excel
- Data Modeling
- Data Visualization

## 6. Data Preparation and Transformation

The dataset was imported into Power BI and processed using Power Query.

Major activities included:
- Checking duplicate transaction identifiers.
- Identifying missing and blank values.
- Correcting date and numerical data types.
- Converting Postal Code into Text.
- Creating a Delivery Days calculated column.
- Cleaning and standardizing return information.
- Preparing regional manager information.
- Creating dimension tables for customers, products, regions, orders, and dates.

## 7. Data Model

The project uses a dimensional data model consisting of fact and dimension tables.

**Fact Tables:**
- FactOrders
- FactReturns

**Dimension Tables:**
- DimCustomer
- DimProduct
- DimRegion
- DimOrder
- DimDate

The model uses relationships between unique dimension keys and corresponding transaction records to support filtering and analysis.

## 8. Dashboard Pages

### Page 1 – Executive Overview
Displays total sales, total profit, total orders, profit margin, monthly sales trends, and customer segment performance.

### Page 2 – Sales and Product Analysis
Analyzes category-wise sales, sub-category profitability, top-performing products, quantity, and discount patterns.

### Page 3 – Regional Analysis
Provides insights into regional sales, market performance, geographic distribution, and regional manager performance.

### Page 4 – Operations and Returns
Analyzes shipping modes, average delivery days, returned orders, return rates, and order priorities.

## 9. Expected Business Outcomes

The dashboard helps identify business growth trends, profitable product categories, loss-making sub-categories, customer segment contributions, and regional performance differences.

It also provides insights into shipping efficiency and returned orders, helping management identify opportunities for operational improvement.

## 10. Author

**Poorvika HV**

## 11. Disclaimer

This project was developed for educational and portfolio purposes. Dataset ownership and redistribution rights remain with their respective owners. The analysis represents the historical dataset period and should not be interpreted as current business performance.