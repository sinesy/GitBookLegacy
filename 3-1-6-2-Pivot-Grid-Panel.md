# Pivot Grid

In this type of grid, columns can be grouped according to their usage/meaning. In order to make it clear, let’s see a typical example, where there is a table storing a list of order rows, where each row is related to products with variants, i.e. products having the same code but different variants, like color, size, etc..  
Such a kind of table could have columns like these ones:

* ROW\_NUM \(PRIMARY KEY\)
* ORDER\_YEAR \(FK TO ORDERS\)
* ORDER\_NUM \(FK TO ORDERS\)
* PRODUCT\_CODE
* COLOR\_CODE
* SIZE\_CODE
* QTY
* UNIT\_PRICE

For this example, PRODUCT\_CODE and COLOR\_CODE would be " **pivot columns"** , whereas SIZE\_CODE would be the " **identifying column** " and QTY the " **grouping column** ".  
That means that multiple records related to the same combination ofPRODUCT\_CODE and COLOR\_CODE should be joined to a single raw, where the QTY is reported many times, one for each different value of SIZE\_CODE.  
Basically, theSIZE\_CODE is spread along the columns of the grid.

![](http://4wsplatform.org/wp-content/uploads/2015/12/Schermata-2017-11-22-alle-07.39.04-1024x580.png)

Moreover, records read from a table shoud be grouped not only by PRODUCT\_CODE and COLOR\_CODE, but also by ORDER\_YEAR and ORDER\_NUM.  
ROW\_NUM is not needed to the grid, since it value changes according to the real record in the database: remember that N records stored in the database table are showed in a single row in grid \(if they have the same PRODUCT\_CODE and COLOR\_CODE\).  
Anyway, ROW\_NUM must be declared as a "managed column", otherwise its value would not be generated when saving records to the database.  
Starting from this example, it is now time to see how to configure a pivot table. Once selected the "pivot grid" from the "Add window" wizard, the user has to define settings for the grid. In addition, for a pivot grid the user also has to define settings related to that grid component:

* business component that defines the list of columns for pivot column group, the only field specified in the select clause is used to automatically create the pivot column \(this setting is mandatory\). The number of pivot columns is the count of the list of element of business component
* business component that defines the header of pivot column group, the fields specified in the select clause are used to automatically set the header of pivot column, the fields specified are like , \(comma\)

Other fields are not considered.

Apart from these settings, required while creating the pivot grid component, it is needed to specify three additional settings in the list of columns:

* the column named " **Pivot Columns** " requires to check at least one field to use as a pivot column, i.e. the list of fields that identify a single row in the grid \(i.e. they are used to group multiple records in one row in grid\); for instance, if a row shows a list of sizes for a product having a specific item name and color, then the item code and color represent the pivot fields, whereas the size must be showed along the columns of the grid; the result is the execution of the SQL query linked to the grid with the additional group by clause composed by all the pivot fields.

Consequently, never define the identifying column as part of the “pivot columns”.

* the column named " **Aggregated column** " represents the quantity to show for each column; in the example above, it can be a quantity or a price related to each size; you have to define at least one field as an aggregate column; all aggregated columns are mandatory.
* the column named " **Identifying Column** " represents the field to show along the grid columns; in the example above, it is the size; consequently, the set of records read from the database and related to the same combination of item and color becomes one only row in grid, where each record reading becomes a specific size and the corresponding quantity is reported as its cell value.

---



