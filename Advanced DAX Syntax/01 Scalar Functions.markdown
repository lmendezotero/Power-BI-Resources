## Advanced DAX Scalar Functions 

Scalar functions return a single value, rather than a column or table.

### A. Aggregation Functions

#### 1. SUM()
Evaluates the sum of a column.
Syntax for SUM():

= SUM(ColumnName)

#### 2. AVERAGE()
Returns the average (arithmetic mean) of all the numbers in a column.
Syntax for AVERAGE():

= AVERAGE(ColumnName)

#### 3. MAX()
Returns the largest value in a column or between two scalar expressions.
Syntax for MAX():

= MAX(ColumnName) or
= MAX(Scalar1, Scalar1)

#### 4. MIN()
Returns the smallest value in a column or between two scalar expressions.
Syntax for MIN():

= MIN(ColumnName) or
= MIN(Scalar1, Scalar1)

#### 5. COUNT()
Counts the number of cells in a column that contain numbers.
Syntax for COUNT():

= COUNT(ColumnName)

#### 6. DISTINCTCOUNT()
Counts the number of distinct or unique values in a columns.
Syntax for DISTINCTCOUNT():

= DISTINCTCOUNT(ColumnName)

#### 7. COUNTROWS()
Counts the number of rows in the specified table, or a table defined by an expression.
Syntax for COUNTROWS():

= COUNTROWS(Table)

Important Note: For large datasets (1M + rows) using COUNTROWS and VALUES may put less strain on the DAX engines than DISTINCTCOUNT.
Difference between SUM vs SUMX


