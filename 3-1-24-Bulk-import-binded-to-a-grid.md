Platform provides a feature to import a list of data, expressed in .xls or .csv format and connected to a grid. This import function can be enabled through the "Import file configuration" menu item. When creating a new configuration, a table and its related grid must be specified. Import task will be then connected to that grid and table. Once defined this import task, it can be accessed in the web interpreter, when opening the grid panel: an import button will be added to the grid’s toolbar and used to select the import task to start, from the list of tasks related to that grid: any number of tasks can be configured, so different import profiles can be defined for the same grid, each with specified default values and import file format.
When defining the configuration, it is possible to chose between two alternative file formats and according to that, different settings are needed:

* xls; it requires to specify the starting line number, since the excel document could contain one or more header lines for columns description; it is possible to specify which folder has to be taken into account
* csv; in that case, the fields separato must be specified (e.g. , or ; )

Once saved those settings, the fields list will be refreshed; you have to chance to map each table field with a rule to use to fill it, through the "Expression column". It is possible to fill in that column with:
a constant value &#8211; a number, a text or a date; in case of date, it must be expressed in the default format yyyy-MM-dd HH:mm:ss
or with a predefined function

The list of allowed functions is reported below:
COLUMN_XXX, where XXX is a number starting from 0 in case of CSV or A, B, C, … in case of Excel columns; it represents the column in the file to read
PROGRESSIVE(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; it generates a counter for that field and checks if the record identified by the list of fields is already stored in the destination table: in that case, the insertion is skipped
GET_VALUE(SQL,FIELDNAME1,FIELDNAME2,&#8230;) &#8211; retrieves the value for the field by executing the specified SQL query; the SQL statement can contain :XXX variables or references to importing fields, expressed as binding variables ?, fields to use to bind to ? must follow the SQL statement, separated by commas;
## Example
GET_VALUE(SELECT ID FROM CLIENTS WHERE NAME=:XXX AND FIELD=?,COLUMN_X,&#8230;)
In this example, the function requires multiplearguments, starting from the SQL query to execute. The where condition contains dynamic conditions which can be expressed in two alternative ways:

* as a global predefined variable, expressed as :XXX where XXX is a Platform variable name (e.g. :USERNAME, etc.), predefined or custom
* as a parameter whose value comes from another cell of the same input row; in this case, the condition is expressed through a ? and the corresponding value must be defined as an additional argument of the GET_VALUE function (hence separated by a comma)


:XXX &#8211; where XXX is a Platform variable name (e.g. :USERNAME, etc.)
FILE_NAME &#8211; input file name
CONCAT(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; concatenate the list of fields or other constants
ADD(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; sum two numbers
DIVIDE(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; divide two numbers
MULTIPLY(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; multiply two numbers
REMAINDER(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; calculate the mod of two numbers
SUBTRACT(FIELDNAME1,FIELDNAME2,&#8230;) &#8211; substract two numbers
UPPER(FIELDNAME) &#8211; make the field value to uppercase
LOWER(FIELDNAME) &#8211; make the field value to lowercase
SUBSTRING(FIELDNAME,NUM1,NUM2) &#8211; calculate the substring of the specified value, starting from the NUM1 index to NUM2 index (excluded)
LENGTH(FIELDNAME) &#8211; calculate the length of the value identified by the specified field name
RIGHT(FIELDNAME,NUM1) &#8211; calculate the substring of the specified value, starting from the end, for a number of characters defined by NUM1; e.g. RIGHT(FIELDXX,2) gets the last two characters of the string
TRIM(FIELDNAME) &#8211; remove left and right spaces from the string value
LTRIM(FIELDNAME) &#8211; remove left spaces from the string value
RTRIM(FIELDNAME) &#8211; remove right spaces from the string value
LPAD(FIELDNAME,NUM) &#8211; add spaces to the left of the string value, until the whole string will reach NUM characters
RPAD(FIELDNAME,NUM) &#8211; add spaces to the right of the string value, until the whole string will reach NUM characters

 **Events supported while importing rows in grid** 
There are a few events which can be configured in the grid and invokable when importing data from a csv or xls file:

*  **Before importinga row** 
*  **After importing a row** 
*  **Before importingall rows** 
*  **After importing all rows** 

The action to link to these events MUST be a server-side js action.
In case of &#8220; **Before importing a row** &#8221; event, the js action will have in input a  **vo**  variable, containing the values of the current row under process. That js object contains all the value read from the input file and you can override some of them through the method:
utils.setAttributeName(&#8220;COLUNM_XXX&#8221;,value);

That row has not been inserted yet, so that you can skip its processing, by launch an instruction like:


```js
throw "message";
```


values in the vo variable are expressed in two alternative ways, according to the file in input:

* in case of an xls file, vo attributes are: COLUMN_A, COLUMN_B, &#8230;
* in case of an csvfile, vo attributes are: COLUMN_0, COLUMN_1, &#8230;


In case of &#8220; **After importing all rows** &#8221; event, the js action will have in input a  **vo**  variable, containing an attribute named &#8220; **importedRows** &#8221; reporting the number of processed rows.


 **How to manage the insert/update of records whose primary key is a progressive** 
In case you need to fill a table whose primary key is a progressive reckoned through an application table, you cannot use the GET_VALUE or PROGRESSIVE functions, since the first can only get back a value, not change it and the second function can only work with progressives determined through an internal counter directly managed by Platform.
If you have your own application table used to get the current value for a progressive, the PROGRESSIVE function cannot help you.
In such a scenario, you can use the &#8220;before import row&#8221; event and link to it a server-side js action whose content should include:

*  **var json = utils.executeQuery(&#8220;SELECT YOUR_PKFROM YOUR_TABLE WHERE YOUR_PK = &#8230; &#8220;, yourdatasourceId, false, true, []);** 

here you have to check out whether the record to import already exists: if it is already stored in the table, then get the current value for the PK, otherwise execute the following instructions to generate a new value for the progressive&#8230;

*  **utils.executeSql(&#8220;UPDATE YOUR_PROGRESSIVES_TABLE SET CURRENTVALUEFIELD =CURRENTVALUEFIELD + &#8230; WHERE CONDITIONS&#8230;&#8221;, yourdatasourceId, false, true, []);** 

this instruction will increase the current value in your application table where the progressive is stored

*  **var json = utils.executeQuery(&#8220;SELECT CURRENTVALUEFIELD FROMYOUR_PROGRESSIVES_TABLE WHERE CONDITIONS&#8230;&#8221;, yourdatasourceId, false, true, []);** 

here you have to fetch the current value to set to your progressive.
At this point, you have a progressive: either fetchedfrom the first query or generated through the last two instructions. The next step is to pass it back to the mapping procedure, through the following command:

*  **utils.setAttribute(&#8220;COLUMN_XYZ&#8221;, yourprogressive);** 

be sure that COLUMN_XYZ does not exists in the input file, so you can set it as you wish

* finally, in the mapping between input fields and table fields in output, you have to map COLUMN_XYZ with your YOUR_PK field, so that the value is correctly set to the record to insert/update. The insert/update operations will do the rest!


                

---


