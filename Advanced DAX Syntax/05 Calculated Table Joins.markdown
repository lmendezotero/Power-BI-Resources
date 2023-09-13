## Calculated Table Join Functions

Calculated table joins are used to combine two or more tables of data. Common examples include CROSSJOIN, UNION, EXCEPT and INTERSECT.

Common use cases:
* Blending or combining data across multiple tables.
* Creating advanced calculations like new vs returning users or repeat purchase behavior.
* Querying tables to troubleshoot or better understand relationships in a data model.

#### 1. CROSSJOIN()
Returns a table that contains the cartesian (product of two sets, formatting a new set containing all ordered pairs) product of the specified tables.
Syntax for CROSSJOIN():

    = CROSSJOIN(Table, Table, […])

Some examples about tables created using CROSSJOIN():

    CROSSJOIN Demo = 
    CROSSJOIN(
        VALUES(
            'Product Lookup'[product_category]
        ),
        VALUES(
            'Product Lookup'[product_group]
        ),
        FILTER(
            VALUES( 'Store Lookup'[store_id]),
            'Store Lookup'[store_id] = 5
        )
    )

#### 2. UNION() 
It combines or “stacks” rows from two or more tables sharing the same column structure.
Syntax for UNION():

    = UNION(Table, Table, […])

Important Note! UNION stacks tables together, just like append!

Some examples about tables created using UNION():

    Target Sales - March 2019 Constructor Demo = 
    DATATABLE(
        "Store ID", INTEGER,
        "Year", STRING,
        "Month", STRING,
        "Bean/Teas Goal", INTEGER,
        "Beverage Goal", INTEGER,
        "Food Goal", INTEGER,
        "Merchandise Goal", INTEGER,
        {
            {3,"2019","March",211,12703,1595,53},
            {5,"2019","March",254,12451,1696,81},
            {8,"2019","March",306,12474,1633,17}
        }

    )

    Target Sales - April 2019 Constructor Demo = 
    DATATABLE(
        "Store ID", INTEGER,
        "Year", STRING,
        "Month", STRING,
        "Bean/Teas Goal", INTEGER,
        "Beverage Goal", INTEGER,
        "Food Goal", INTEGER,
        "Merchandise Goal", INTEGER,
        {
            {3,"2019","April",268,15608,1964,80},
            {5,"2019","April",277,14687,2020,91},
            {8,"2019","April",377,15011,1973,34}
        }

    )

    UNION Demo = 
    UNION(
        'Target Sales - March 2019 Constructor Demo',
        'Target Sales - April 2019 Constructor Demo'    
    )

#### 3. EXCEPT() 
It returns all rows from the left table which do not appear in the right table.

![alt text](https://github.com/lmendezotero/Power-BI-Resources/blob/main/Advanced%20DAX%20Syntax/Pictures/EXCEPT_Result.png)

Syntax for EXCEPT():

    = EXCEPT(LeftTable, RightTable)

As we can see, using the EXCEPT function is a similar way of obtaining the same table but with some filters applied. 

Some examples about tables created using EXCEPT():

    EXCEPT Demo = 
    EXCEPT(
        'Customer Lookup',
        FILTER(
            VALUES(
                'Customer Lookup'
            ),
            'Customer Lookup'[customer_since] > DATE(2017,02,01)
        )
    )


#### 3. INTERSECT()
It returns all the rows from the left table which also appear in the right table.

![alt text](https://github.com/lmendezotero/Power-BI-Resources/blob/main/Advanced%20DAX%20Syntax/Pictures/INTERSECT_Result.png)

Syntax for INTERSECT():

    = INTERSECT (LeftTable, RightTable)

Some examples about tables created using INTERSECT()

    INTERSECT Demo = 
    INTERSECT(
        ADDCOLUMNS(
        'Employee Lookup',
        "Revenue",
        [Customer Sales]
        ),
        ADDCOLUMNS(
        FILTER(
            'Employee Lookup',
            'Employee Lookup'[start_date] > DATE(2016,12,31)
        ),
        "Revenue",
        [Customer Sales]
        )
    )
