# DAX Measures and Calculations

This document records the calculations used in the Global Superstore
Power BI report. Confirm that the table and column names match the final
model before using each expression.

## 1. Core KPI measures

``` dax
Total Sales =
SUM(FactOrders[Sales])
```

``` dax
Total Profit =
SUM(FactOrders[Profit])
```

``` dax
Total Orders =
DISTINCTCOUNT(FactOrders[Order ID])
```

``` dax
Total Customers =
DISTINCTCOUNT(FactOrders[Customer ID])
```

``` dax
Total Quantity =
SUM(FactOrders[Quantity])
```

``` dax
Profit Margin =
DIVIDE([Total Profit], [Total Sales], 0)
```

``` dax
Average Order Value =
DIVIDE([Total Sales], [Total Orders], 0)
```

## 2. Time intelligence

These measures require an active relationship from `DimDate[Date]` to
`FactOrders[Order Date]`, and `DimDate` must be marked as the model's
date table.

``` dax
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

``` dax
Sales YoY Growth % =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

``` dax
Previous Year Profit =
CALCULATE(
    [Total Profit],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

``` dax
Profit YoY Growth % =
DIVIDE(
    [Total Profit] - [Previous Year Profit],
    [Previous Year Profit],
    0
)
```

## 3. Product and discount analysis

``` dax
Average Discount =
AVERAGE(FactOrders[Discount])
```

``` dax
Sales per Unit =
DIVIDE([Total Sales], [Total Quantity], 0)
```

``` dax
Loss Making Sales =
CALCULATE(
    [Total Sales],
    FactOrders[Profit] < 0
)
```

`Loss Making Sales` sums the sales value of transaction lines whose
profit is negative. It is not the amount of the loss; use a separate
negative-profit measure if you need that.

## 4. Shipping and returns

``` dax
Average Delivery Days =
AVERAGE(FactOrders[Delivery Days])
```

``` dax
Returned Orders =
CALCULATE(
    DISTINCTCOUNT(FactReturns[Order ID]),
    FactReturns[Returned] = "Yes"
)
```

``` dax
Return Rate =
DIVIDE(
    [Returned Orders],
    [Total Orders],
    0
)
```

**Important model note:** `FactReturns` should be filtered by the
relevant order dimension or another validated relationship. Ensure the
returned-order measure and denominator use the same order population and
filter context. If the return table contains only returned orders,
confirm that the `Returned` value is consistently `"Yes"`.

## 5. Formatting recommendations

  Measure                 Suggested format
  ----------------------- ------------------
  Total Sales             Currency
  Total Profit            Currency
  Total Orders            Whole number
  Total Customers         Whole number
  Total Quantity          Whole number
  Profit Margin           Percentage
  Average Order Value     Currency
  Sales YoY Growth %      Percentage
  Profit YoY Growth %     Percentage
  Average Discount        Percentage
  Average Delivery Days   Decimal number
  Return Rate             Percentage

## 6. Calculated column in Power Query

The `Delivery Days` column is created in Power Query, not DAX:

``` powerquery
Duration.Days([Ship Date] - [Order Date])
```

It calculates the number of calendar days between the order date and
ship date.
