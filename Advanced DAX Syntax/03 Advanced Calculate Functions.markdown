## Advanced DAX Calculate Functions 

### 1. Expanded Tables

An expanded table consists of the base table (which is visible to the user) along with columns from any related table connected via a 1-to-1 or many-to-1 relationship.



Expanded tables in data models always go from the MANY side (fact tables) to the ONE side (look up table) of the relationship.



In the previous example, the expanded version of the AW_Sales table contains all fields from the product, subcategory and category lookup tables.

### 2. Context Transitions

#### 2.1 Context Transition in Calculated Columns
Context transition is the process of turning row context into filter context.
* By default, calculated columns understand row context but not filter context.
* To create filter context at the row-level, you can use CALCULATE.

#### 2.1 Context Transition in Measures
In measures, Context transition is automatically applied. So, if we include the formula of SUM(ColumnName) without CALCULATE into a measure, we will get the same results as include CALCULATE becuase the DAX engine calculates the Filter Context to get the correct results. 

### 3. Evaluation Order & Modifiers
In general, the DAX engine evaluates the formulas in the following way when CALCULATE is applied:
* Firts it evaluates the filters.
* Second it evaluates the expressions.

However, when modifiers are applied, the evaluation order changes and the DAX engine will check firstly the modifiers, then the filters and finally the expression.

So, modifiers are used to alter the way CALCULATE creates filter context and are added as filter arguments within a CALCULATE function. Modifers are also used to access inactive table relationships or change the way filters propagate (one-way to bidirectional or biceversa).

#### ALL()
Outside CALCULATE, ALL returns all the rows in a table or all the values in a column, ignoring any filters that might have been applied.

Correct syntax for ALL():

    = ALL(TableName[ColumnName])

For example, outside CALCULATE we can use ALL to create a table with unique values (like a look up table).

Hovewer, inside CALCULATE, ALL is a modifier and it will return all the values from column or all the rows from table ignoring all the filters applied (both in visuals and in tables).


#### REMOVEFILTERS()
REMOVEFILTERS returns all the rows from a table or all the values from several columns ignoring any applied filter.
Therefore, REMOVEFILTERS is just an alias of ALL as a CALCULATE modifier, so it works in the same manner, but it is not possible to use REMOVEFILTERS outside CALCULATE.

Correct syntax for REMOVEFILTERS():

    = CALCUALATE(
        Expression,
        REMOVEFILTERS(TableName[ColumnName],[...])
    )

Example of % Total Calculation with REMOVEFILTERS():

    % of Store Sales (REMOVEFILTERS) = 
    VAR AllStoreSales = 
    CALCULATE(
        [Customer Sales],
        REMOVEFILTERS('Store Lookup'[store_id])
    )
    VAR Ratio = 
    DIVIDE(
        [Customer Sales],
        AllStoreSales
    )
    RETURN Ratio

#### KEEPFILTERS()
KEEPFILTERS allows you to control which filters get applied to a calculation.
This function plays a role in determining which rows should, or should not be considered by the calculation, in the same way, a WHERE clause impacts a T-SQL statement.

Correct syntax for KEEPFILTERS():



### 4. COMMON TOTAL PATTERNS FOR CALCULATE

Example of *Cumulative Total* using ALL():

    Cumulative Total = 
    CALCULATE(
        SUM(
            'Sales by Store'[quantity_sold]
        ),
        FILTER(
            ALL(
                'Calendar'[transaction_date]
            ),
            'Calendar'[transaction_date] >= MAX('Calendar'[transaction_date])
        )
    )

Example of *Overall Total* using ALL():

    Overall Total = 
    CALCULATE(
        SUMX(
            'Sales by Store',
            'Sales by Store'[unit_price] * 'Sales by Store'[quantity_sold]
        ),
        ALL(
            'Sales by Store'
        )
    )

Example of *Percent of Total* using ALL():

    Percent of Total = 
    VAR _CurrentSales = 
    SUMX(
        'Sales by Store',
        'Sales by Store'[unit_price] * 'Sales by Store'[quantity_sold]
    )

    VAR _CurrentSales =
    CALCULATE(
        SUMX(
            'Sales by Store',
            'Sales by Store'[unit_price] * 'Sales by Store'[quantity_sold]
        ),
        ALL(
            'Sales by Store'
        )
    ) 

    VAR _Ratio = 
    DIVIDE(
        _CurrentSales,_CurrentSales
    )

    RETURN
    _Ratio