# DAX Measures and Calculations

## 1. Introduction

DAX (Data Analysis Expressions) was used in Power BI to create measures and calculations for business performance analysis.

These calculations support KPI cards, sales comparisons, profitability analysis, time intelligence, product analysis, and operational reporting.

## 2. Sales and Profitability Measures

### Total Sales

```dax
Total Sales =
SUM(FactOrders[Sales])
```

Calculates the total sales revenue.

### Total Profit

```dax
Total Profit =
SUM(FactOrders[Profit])
```

Calculates the overall profit generated.

### Total Orders

```dax
Total Orders =
DISTINCTCOUNT(FactOrders[Order ID])
```

Counts unique customer orders.

### Total Customers

```dax
Total Customers =
DISTINCTCOUNT(FactOrders[Customer ID])
```

Counts unique customers.

### Total Quantity

```dax
Total Quantity =
SUM(FactOrders[Quantity])
```

Calculates the total quantity of products sold.

### Profit Margin

```dax
Profit Margin =
DIVIDE([Total Profit], [Total Sales], 0)
```

Calculates profit as a percentage of sales.

### Average Order Value

```dax
Average Order Value =
DIVIDE([Total Sales], [Total Orders], 0)
```

Calculates the average sales value per order.

## 3. Time Intelligence Measures

### Previous Year Sales

```dax
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

Calculates sales for the corresponding period in the previous year.

### Sales YoY Growth %

```dax
Sales YoY Growth % =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

Calculates year-over-year sales growth.

### Previous Year Profit

```dax
Previous Year Profit =
CALCULATE(
    [Total Profit],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

Calculates profit for the corresponding period in the previous year.

### Profit YoY Growth %

```dax
Profit YoY Growth % =
DIVIDE(
    [Total Profit] - [Previous Year Profit],
    [Previous Year Profit],
    0
)
```

Calculates year-over-year profit growth.

## 4. Product and Discount Analysis

### Average Discount

```dax
Average Discount =
AVERAGE(FactOrders[Discount])
```

Calculates the average discount across transaction rows.

### Sales per Unit

```dax
Sales per Unit =
DIVIDE([Total Sales], [Total Quantity], 0)
```

Calculates average sales value per unit sold.

### Loss Making Sales

```dax
Loss Making Sales =
CALCULATE(
    [Total Sales],
    FactOrders[Profit] < 0
)
```

Calculates the sales value associated with transaction rows that generated negative profit.

## 5. Shipping and Returns Measures

### Average Delivery Days

```dax
Average Delivery Days =
AVERAGE(FactOrders[Delivery Days])
```

Calculates the average number of days between order date and ship date.

### Returned Orders

```dax
Returned Orders =
CALCULATE(
    DISTINCTCOUNT(FactReturns[Order ID]),
    FactReturns[Returned] = "Yes"
)
```

Counts distinct returned orders.

### Return Rate

```dax
Return Rate =
DIVIDE(
    [Returned Orders],
    [Total Orders],
    0
)
```

Calculates the percentage of returned orders against total orders.

## 6. DAX Concepts Used

The project demonstrates the following DAX concepts:

- SUM – Aggregation of numerical values.
- DISTINCTCOUNT – Counting unique identifiers.
- AVERAGE – Calculating average values.
- CALCULATE – Modifying filter context.
- DIVIDE – Safe division with an alternate result.
- SAMEPERIODLASTYEAR – Time intelligence.
- Measure-based KPI calculations.
- Percentage and profitability calculations.

## 7. Measure Formatting

| Measure | Format |
|---|---|
| Total Sales | Currency |
| Total Profit | Currency |
| Total Orders | Whole Number |
| Total Customers | Whole Number |
| Total Quantity | Whole Number |
| Profit Margin | Percentage |
| Average Order Value | Currency |
| Sales YoY Growth % | Percentage |
| Profit YoY Growth % | Percentage |
| Average Discount | Percentage |
| Average Delivery Days | Decimal Number |
| Return Rate | Percentage |

## 8. Important Model Considerations

- DimDate must be marked as the date table.
- DimDate[Date] should have an active relationship with FactOrders[Order Date].
- Dimension keys must be unique on the one side of relationships.
- FactReturns should connect to FactOrders through a validated order-level dimension.
- Return Rate should use a consistent order population and filter context.

## 9. Conclusion

DAX measures helped convert transactional information into meaningful performance indicators. These calculations support interactive analysis of sales, profitability, customers, products, shipping, and returns.