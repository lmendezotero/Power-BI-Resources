## Advanced DAX Scalar Functions 

Scalar functions return a single value, rather than a column or table.

![alt text](https://github.com/lmendezotero/Power-BI-Resources/blob/main/Advanced%20DAX%20Syntax/Pictures/Scalar_Functions.png)

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

    = MAX(ColumnName) 
    or
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


### B. Rounding Functions

#### 1. INT()
Rounds a number down to the nearest integer.
Syntax for INT():

    = INT(Number)

#### 2. ROUND()
Rounds a number to a specific number of digits.
Syntax for ROUND():

    = ROUND(Number, NumberOfDigits)

#### 3. ROUNDUP()
Rounds a number up, away from zero.
Syntax for ROUNDUP():

    = ROUNDUP(Number, NumberOfDigits)

#### 4. ROUNDDOWN()
Rounds a number down, toward zero.
Useful function to specify the precision of a number, like customer age.
Syntax for ROUNDDOWN():

    = ROUNDOWN(Number, NumberOfDigits)

#### 5. MROUND()
Rounds a number to the desired multiple.
Useful function for dates or to create groups/beans of data.
Syntax for MROUND():

    = MROUND(Number, Multiple)

#### 6. TRUNC()
Truncates a number to a integer by removing the decimal part of the number.
Syntax for TRUNC():

    = TRUNC(Number, NumberOfDigits)

#### 7. FIXED()
Round a number to an integer by removing the decimal part of the number.
Useful function when you want to convert a number to text.
Syntax for FIXED():

    = FIXED(Number, Decimals)

#### 8. CEILING()
Rounds a number up, to the nearest integer or nearest until of significance.
Useful function for dates or to create groups/beans of data.
Syntax for CEILING():

    = CEILING(Number, Significance)

#### 9. FLOOR()
Rounds a number down, toward zero, to the nearest multiple of significance.
Useful function for dates or to create groups/beans of data.
Syntax for FLOOR():

    = FLOOR(Number, Significance)

### C. Information Functions

#### 1. ISBLANK()
Checks whether a value is blank and returns TRUE or FALSE.
Syntax for ISBLANK():

    = ISBLANK(Value)

#### 2. ISERROR()
Checks whether a value is an error and returns TRUE or FALSE.
Syntax for ISERROR():

    = ISERROR (Value)

#### 3. ISLOGICAL()
Checks whether a value is a logical value (TRUE or FALSE) and returns TRUE or FALSE.
Syntax for ISLOGICAL():

    = ISLOGICAL (Value)

#### 4. ISNUMBER()
Checks whether a value is a number and returns TRUE or FALSE.
Syntax for ISNUMBER():

    = ISNUMBER(Value)

#### 5. ISNONTEXT()
Checks whether a value is not text (blank cells are not text) and returns TRUE or FALSE.
Syntax for ISNONTEXT():

    = ISNONTEXT (Value)

#### 6. ISTEXT()
Checks whether a value is a text and returns TRUE or FALSE.
Syntax for ISTEXT():

    = ISTEXT(Value)

### D. Conversion Functions

#### 1. CURRENCY()
Evaluates the argument and returns the results as a currency data type.
Syntax for CURRENCY():

    = CURRENCY(Value)

#### 2. FORMAT()
Converts a value to text in the specified number format.
Syntax for FORMAT():

    = FORMAT(Value, Format)

#### 3. DATE()
Returns the specified date in datetime format.
Syntax for DATE():

    = DATE(Year, Month, Day)

#### 4. TIME()
Converts hours, minutes and seconds given as numbers to a time in datetime format.
Syntax for TIME():

    = TIME(Hours, Minute, Second)

#### 5. DATEVALUE()
Convert a date in the form of text to a date in datetime format.
Syntax for DATEVALUE():

    = DATEVALUE(DateText)

#### 6. VALUE()
Converts a text string that represent a number to a number.
Syntax for VALUE():

    = VALUE(Text)


### E. Logical Functions
The most common logical functions are IF(), AND() y OR().

#### 1. IF()
Checks if a given condition is met, and returns one value if the condition is TRUE, and another value if the condition is FALSE.
Syntax for IF():

    = IF(LoficalTest, ResultIfTrue, [ResultIfFalse])

#### 2. AND()
Checks whether both arguments are TRUE, and returns TRUE if both arguments are TRUE, otherwise returns FALSE.
Syntax for AND():

    = AND(Logical1, Logical2)

Note: Use the && and || operators if you want to include more than two conditions!

#### 3. OR()
Checks whether one of the arguments is TRUE to return TRUE, and returns FALSE if both arguments are FALSE.
Syntax for OR():

    = OR(Logical1, Logical2)

Note: Use the && and || operators if you want to include more than two conditions!

#### 4. SWITCH()
Evaluates an expression against a list of values and returns one of multiple possible expressions.
Syntax for SWITCH():

    = SWITCH(Expression, Value1, Result1, …, [Else])

    = SWITCH(TRUE(), Value1, Result1, …, [Else])

#### 5. COALESCE()
Returns the first argument that does not evaluate to BLANK. If all arguments evaluate to BLANK, BLANK is returned.
Syntax for COALESCE():

    = COALESCE(Expression1, Expression2, […])


