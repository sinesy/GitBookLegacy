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
* business component that defines the header of pivot column group, the fields specified in the select clause are used to automatically set the header of pivot column, the fields specified are like , \(comma\); **the first field in the select must be the code related to "identifying column"** \(in the example above, the CODE\_SIZE\); optionally, the select can contain  a second field, which will be used to set the column headers with these values rather than the codes; if the second field in the select is not specified, the first will be used to set the column headers; that means **the column headers are set with codes as default behavior and optionally they can be set with a description contained in the second field of the select clause**.

Other fields are not considered.

Apart from these settings, required while creating the pivot grid component, it is needed to specify three additional settings in the list of columns:

* the column named " **Pivot Columns** " requires to check at least one field to use as a pivot column, i.e. the list of fields that identify a single row in the grid \(i.e. they are used to group multiple records in one row in grid\); for instance, if a row shows a list of sizes for a product having a specific item name and color, then the item code and color represent the pivot fields, whereas the size must be showed along the columns of the grid; the result is the execution of the SQL query linked to the grid with the additional group by clause composed by all the pivot fields.

Consequently, never define the identifying column as part of the “pivot columns”.

* the column named " **Aggregated column** " represents the quantity to show for each column; in the example above, it can be a quantity or a price related to each size; you have to define at least one field as an aggregate column; all aggregated columns are mandatory.
* the column named " **Identifying Column** " represents the field to show along the grid columns; in the example above, it is the size; consequently, the set of records read from the database and related to the same combination of item and color becomes one only row in grid, where each record reading becomes a specific size and the corresponding quantity is reported as its cell value.



**Behind the scenes**

When saving data in update, edited cell can lead to 3 scenarios:

* the edited cell was empty and it was filled out with a number &gt; 0; this is managed as an INSERT
* the edited cell was not empty and with a value different from 0 
  * and then cleared up or set to 0; this is managed as a DELETE
  * and then changed with another value different from 0; this is managed as an UPDATE

In order to correctly execute these operations, the grid must be configured by taking into account also mandatory values in the table where saving data:

* in case of INSERT, you have to correctly set "default values in insert" for each mandatory field and these fields must be set as "to manage. In case the pk fields or other mandatory fields are not set starting from the UI or from default values \(as for an internal counter\), you can always use the "before save data in insert" event and link a server-side javascript action to fill in these values, through the method utils.setAttributeValue\(attrName,value\)
* in case of UPDATE, you have to correctly set "default values in update" for each mandatory field not retrieved from the input, and these fields must be set as "to manage"; you have the chance to omit some fields \(flag "to manage" set to false\) for not mandatory fields: these fields will be ignored during the UPDATE operation, and the previous value would be maintained. In case other mandatory fields are not set starting from the UI or from default values, you can always use the "before save data in update" event and link a server-side javascript action to fill in these values, through the method utils.setAttributeValue\(attrName,value\)
* for UPDATE/DELETE fields, you have to provide the values for the "real" primary key, otherwise it would be impossible to execute the operation. Behind the scenes, Platform always try to fetch the whole "real" record from the database, starting from the "pivot column values", which are considered "unique" and therefore they allow to get a single record from the database. The record fetched is used to fill in the pk in UPDATE/DELETE, if not included in the "pivot columns"; in case of UPDATE operation, the fetch operation is also used to fill in other fields \(not belonging to the pk\) and not available in the grid, but only for the fields marked as "to manage".





---



