When selecting the "Grid Data Import" execution type, two additional input parameters must be defined in the "Params" folder:
 **UPDATE**  &#8211; this parameter can accept two alternative values:  **Y**  or  **N** ; if set to Y, then the import process will try to update records already existings and insert the rows from input not still stored in the table; if set to N, then all input rows will be managed as insert SQL statements and the import process could fail if one or more records are alreadt stored in the table to load.
 **FILE_NAME**  &#8211; file name related to the source file to read and containing the data to load in the table. It can be a csv or a cls file, according to what defined in the import task.
See also &#8220;Bulk import binded to a grid&#8221; for more information about the configuration of a data import in grid.


                

---


