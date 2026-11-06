# Data Cleaning Log

## Dataset

Source workbook: `Global Superstore.xls`\
Power Query queries: `FactOrders`, `FactReturns`, `DimRegionalManager`

> Record the actual actions and results from your Power Query session.
> Do not claim that an issue was found or fixed unless you verified it
> in the source data.

## 1. FactOrders

  ---------------------------------------------------------------------------------------------
  Check / transformation  Action                  Validation / notes
  ----------------------- ----------------------- ---------------------------------------------
  Query name              Renamed `Orders` to     Confirmed in Queries pane
                          `FactOrders`            

  Row ID                  Checked for duplicate   Record duplicate count and action below
                          identifiers             

  Order ID                Checked for null or     Record count and treatment below
                          blank values            

  Order Date              Set data type to Date   Verify no conversion errors

  Ship Date               Set data type to Date   Verify no conversion errors

  Sales                   Set data type to        Verify values
                          Decimal Number          

  Profit                  Set data type to        Verify values
                          Decimal Number          

  Discount                Set data type to        Verify values
                          Decimal Number          

  Shipping Cost           Set data type to        Verify values
                          Decimal Number          

  Quantity                Set data type to Whole  Verify values
                          Number                  

  Postal Code             Set data type to Text   Preserves identifier formatting

  City, Country,          Checked for null /      Investigate before removing records
  Category, Segment,      blank values            
  Region                                          

  Delivery Days           Added custom column     `Duration.Days([Ship Date] - [Order Date])`
  ---------------------------------------------------------------------------------------------

### FactOrders validation notes

-   Do not remove repeated `Order ID` values simply because they repeat:
    an order can contain multiple product lines.
-   Use `Row ID` to investigate duplicate transaction rows.
-   Investigate negative delivery-day values and conversion errors.
-   Missing postal codes are not, by themselves, a reason to delete a
    transaction.

**Observed row count before cleaning:** \[Fill in\]\
**Observed row count after cleaning:** \[Fill in\]\
**Duplicate Row ID count:** \[Fill in\]\
**Null / blank Order ID count:** \[Fill in\]\
**Other issues and resolutions:** \[Fill in\]

## 2. FactReturns

  -----------------------------------------------------------------------
  Check / transformation  Action                  Validation / notes
  ----------------------- ----------------------- -----------------------
  Query name              Renamed `Returns` to    Confirmed in Queries
                          `FactReturns`           pane

  Order ID                Checked for null /      Record count and
                          blank values            treatment

  Duplicate Order ID      Inspected repeated      Confirm return statuses
                          order identifiers       agree before
                                                  deduplication

  Returned                Applied Trim and Clean; Confirm standardized
                          checked distinct values values

  Columns                 Retained `Order ID` and Verify final columns
                          `Returned`              
  -----------------------------------------------------------------------

**Observed row count before cleaning:** \[Fill in\]\
**Observed row count after cleaning:** \[Fill in\]\
**Duplicate Order ID count:** \[Fill in\]\
**Conflicting return statuses:** \[Fill in\]

Do not use **Keep Duplicates** as a final cleaning step. It is only an
inspection step; remove that temporary step before continuing. Do not
remove repeated order IDs if they represent conflicting or meaningful
records without investigating them.

## 3. DimRegionalManager

  -----------------------------------------------------------------------
  Check / transformation  Action                  Validation / notes
  ----------------------- ----------------------- -----------------------
  Query name              Renamed `People` to     Confirmed in Queries
                          `DimRegionalManager`    pane

  Region                  Checked for null /      Record findings
                          blank values            

  Region uniqueness       Checked that each       Resolve conflicts
                          region maps to one      before deduplication
                          manager                 

  Person                  Renamed to              Confirmed
                          `Regional Manager`      
  -----------------------------------------------------------------------

The regional manager data was merged into `DimRegion` using a Left Outer
join on Region. Verify that the merge produced a manager for each
expected region and did not multiply rows.

**Number of regions:** \[Fill in\]\
**Missing manager values:** \[Fill in\]\
**Conflicting region-manager mappings:** \[Fill in\]

## 4. Final validation

-   [ ] No unintended Power Query errors remain.
-   [ ] Data types are correct.
-   [ ] Temporary inspection steps (such as Keep Duplicates) were
    removed.
-   [ ] Row counts were checked before and after transformations.
-   [ ] Relationships use unique keys on the one side.
-   [ ] Missing values were investigated rather than blindly deleted.
