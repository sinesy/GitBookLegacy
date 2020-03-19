# How to define a Grid Data Import

When selecting the "Grid Data Import" execution type, two additional input parameters must be defined in the "Params" folder:  
 **UPDATE**  – this parameter can accept two alternative values:  **Y**  or  **N** ; if set to Y, then the import process will try to update records already existings and insert the rows from input not still stored in the table; if set to N, then all input rows will be managed as insert SQL statements and the import process could fail if one or more records are alreadt stored in the table to load.  
 **FILE\_NAME**  – file name related to the source file to read and containing the data to load in the table. It can be a csv or a cls file, according to what defined in the import task.  
See also “Bulk import binded to a grid” for more information about the configuration of a data import in grid.

---



