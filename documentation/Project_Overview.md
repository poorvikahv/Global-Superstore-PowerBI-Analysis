# Global Superstore -- Business Analytics Dashboard

## 1. Project Overview

This project uses Microsoft Power BI to explore Global Superstore retail
transactions and build an interactive business-performance dashboard.
The analysis focuses on sales, profit, customers, products, geography,
shipping, and returned orders.

## 2. Problem Statement

A retail business needs a clear view of its sales and operational
performance. Transaction-level data can be difficult to interpret
without cleaning, modeling, calculations, and visual summaries. This
project transforms the dataset into an interactive report that helps
users investigate business performance.

## 3. Objectives

-   Monitor total sales, profit, orders, customers, quantity, and profit
    margin.
-   Compare performance across time periods, customer segments,
    products, and regions.
-   Identify high-performing and loss-making products or sub-categories.
-   Explore the relationship between discounts and profitability.
-   Review shipping performance and returned orders.
-   Present findings through interactive report pages.

## 4. Dataset

**Dataset:** Global Superstore\
**Workbook used:** `Global Superstore.xls`\
**Worksheets used:** Orders, Returns, People

The Orders worksheet contains order-line and sales information. Returns
contains return status by order. People contains regional manager
information. Confirm the exact column names and dataset version in the
workbook used for this project.

## 5. Tools and Technologies

-   Microsoft Power BI Desktop
-   Power Query for data cleaning and transformation
-   DAX for measures and calculated columns
-   Microsoft Excel as the source format

## 6. Data Model

The report uses a dimensional model with: - `FactOrders` -- order-line
transactions - `FactReturns` -- returned-order information -
`DimCustomer` -- customer attributes - `DimProduct` -- product
attributes - `DimRegion` -- region and regional manager attributes -
`DimOrder` -- distinct order identifiers - `DimDate` -- calendar
attributes

Relationships should use unique keys on the one side and
transaction/detail rows on the many side. Use single-direction filtering
unless a specific requirement has been tested.

## 7. Report Pages

1.  **Executive Overview** -- headline KPIs and sales trends.
2.  **Sales & Product Analysis** -- category, sub-category, product,
    discount, and profit analysis.
3.  **Regional Analysis** -- geography, market, region, and manager
    performance.
4.  **Operations & Returns** -- shipping mode, delivery days, and
    returns.

## 8. Expected Outcome

The final report provides an interactive view of business performance
and allows users to filter and investigate results. Actual findings and
numerical results are documented in `Business_Insights.md` after
validating the finished report.

## 9. Author

**Poorvika HV**

## 10. Disclaimer

This is an educational portfolio project. Dataset ownership and
redistribution rights remain with the dataset provider. Check the
dataset licence before redistributing the source workbook or publishing
underlying data.
