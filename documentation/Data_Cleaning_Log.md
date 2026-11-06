# Data Cleaning and Transformation Log

## 1. Introduction

Data cleaning and transformation were performed using Power Query in Microsoft Power BI. The purpose was to improve data consistency, correct data types, inspect duplicate records, and prepare the tables for data modeling and visualization.

## 2. FactOrders – Orders Table

**Original Worksheet:** Orders  
**Final Query Name:** FactOrders

### Cleaning and Transformation Activities

| Column | Transformation |
|---|---|
| Row ID | Checked for duplicate identifiers |
| Order ID | Checked for null and blank values |
| Order Date | Changed to Date |
| Ship Date | Changed to Date |
| Sales | Changed to Decimal Number |
| Profit | Changed to Decimal Number |
| Discount | Changed to Decimal Number |
| Shipping Cost | Changed to Decimal Number |
| Quantity | Changed to Whole Number |
| Postal Code | Changed to Text |
| City | Checked for blank values |
| Country | Checked for blank values |
| Category | Checked for blank values |
| Segment | Checked for blank values |
| Region | Checked for blank values |

### Duplicate Validation

The Row ID column was used to inspect duplicate transaction identifiers.

The dataset contained 51,290 transaction rows and no duplicate Row ID values.

Order ID was not used as a duplicate-removal key because one order can contain multiple product transactions.

### Calculated Column – Delivery Days

A custom column named Delivery Days was created using Power Query.

```powerquery
Duration.Days([Ship Date] - [Order Date])
```

This calculates the number of calendar days between the order date and shipping date.

## 3. FactReturns – Returns Table

**Original Worksheet:** Returns  
**Final Query Name:** FactReturns

### Cleaning and Transformation Activities

- Checked Order ID for null and blank values.
- Inspected duplicate Order ID records.
- Standardized the Returned column using Trim and Clean.
- Retained Order ID and Returned for the final table.

### Duplicate Validation

The original Returns worksheet contained 1,173 records and 1,172 distinct Order IDs.

One Order ID appeared more than once. Duplicate records were inspected before deciding whether deduplication was appropriate.

The final table should retain one return record per order only after verifying that the repeated records have consistent return statuses.

## 4. DimRegionalManager – People Table

**Original Worksheet:** People  
**Final Query Name:** DimRegionalManager

### Cleaning and Transformation Activities

- Checked Region for blank values.
- Checked regional uniqueness.
- Verified the relationship between Region and Person.
- Renamed Person to Regional Manager.

Regional manager information was merged into DimRegion using a Left Outer join on Region.

This made regional manager information available for regional performance analysis.

## 5. Data Modeling Preparation

The following dimension tables were created:

- DimCustomer
- DimProduct
- DimRegion
- DimOrder
- DimDate

Relationships were established using corresponding identifier columns.

The model was designed to use one-to-many relationships with single-direction filtering wherever applicable.

## 6. Data Quality Considerations

- Missing Postal Code values were not automatically treated as invalid transactions.
- Repeated Order IDs were not automatically considered duplicate transactions.
- Date and numerical columns were checked for appropriate data types.
- Blank values were investigated before deciding whether records required correction.
- Delivery Days values were checked for errors and unexpected negative durations.

## 7. Conclusion

The cleaning and transformation process prepared the Global Superstore dataset for analysis in Power BI. The resulting tables support sales analysis, profitability calculations, regional comparisons, and operational reporting.