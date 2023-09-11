## Advanced DAX Interator Functions
Iterator functions allow you to loop through the same expression on every row of a table in order to evaluate a single scalar value or derive a new table.
Common use cases:
•	Aggregating a column into a single value.
•	Returning a table of data.


#### 1. SUMX()
Returns the sum of an expression evaluated for each row in a table.
Syntax for SUMX():

= SUMX(Table, Expression)

#### 2. CONCATENATEX()
It evaluates an expression for each row of the table and returns the concatenation of those values in a single string, separated by a delimiter.
Syntax for CONCATENATEX():

= CONCATENATE(Table, Expression, [Delimiter], [OrderBy_Expression], [Order])

Example of the "Full Name Employee" measure with CONCATENATEX():
/***************************************************/
Employee Full Name = 
IF(
    HASONEVALUE('Employee Lookup'[first_name]),
    CONCATENATEX(
    'Employee Lookup',
    'Employee Lookup'[first_name] & " " & 'Employee Lookup'[last_name],
    ",",
    'Employee Lookup'[first_name],
    ASC
    ),
    BLANK()
)
/***************************************************/

#### 3. AVERAGEX() 
It calculates the average (arithmetic mean) of a set of expressions evaluated over a table.
Syntax for AVERAGEX():

= AVERAGEX (Table, Expression)

Important Note! AVERAGE & AVERAGEX do not count dates with zero sales when computing an average. To evaluate an average over a date range that includes dates with no sales, use DIVIDE & COUNTROWS instead.

Example of the calculation of "Moving Average" with AVERAGEX():
/***************************************************/
Moving Average = 
VAR LastTransactionDate = MAX('Calendar'[Transaction_Date])
VAR AverageDay = 30
VAR PeriodInVisual = 
FILTER(
    ALL('Calendar'[Transaction_Date]),
    AND(
        'Calendar'[Transaction_Date] > LastTransactionDate - AverageDay,
        'Calendar'[Transaction_Date] <= LastTransactionDate
    )
)
VAR Output = 
CALCULATE(
    AVERAGEX(
        'Calendar',
        [Customer Sales]
    ),
    PeriodInVisual
)

RETURN
Output
/***************************************************/

#### 4. RANKX()
It returns the ranking of a number in a list of numbers for each row in the table argument.
Syntax for AVERAGEX():

= RANKX(Table, Expression, [Value], [Order], [Ties])

Example of ranking calculation with RANKX() avoinding values in the Total of the visual:
/***************************************************/
Rank of Customer Sales = 
IF(
    HASONEVALUE('Product Lookup'[product_category]),
    RANKX(
    ALL(
        'Product Lookup'[product_category]
    ),
    [Customer Sales]
)
)
/***************************************************/