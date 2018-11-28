# Columns properties

The columns list is an editable list where the user can refine the columns behavior. The default setting is automatically defined by the Web Designer, when creating the grid. During the grid definition, the select clause of the binded business component is analyzed: for each field in the select clause a column is created and added to that list. Column type, header name, mandatory, length, editability in insert/edit modes are automatically set, according to the settings of the database fields: if a database field is mandatory, the column is mandatory, if a database field is part of a primary key, the related column is not editable in edit, and so forth.  
There are a great deal of column properties; in order to make easy the column definition, not all properties are showed, only the most common; it is possible to access to the whole range of properties, by pressing the "Advanced mode" button on the toolbar.

![](http://4wsplatform.org/wp-content/uploads/2015/12/DataFields-1024x483.jpg)

These are all properties defined for a column:

* **To manage**  – flag used to define if the field must be managed, in terms of make it visible, editable and saved
* **To show**  – flag used to define if the column is visible; even if it is declared as not visible, the user can always make it visible when interpreting the application, by switching that settings with right click of the mouse on the column header
* **To show only if**  – boolean expression, in Javascript format, used to dinamically define if the column is to show or not
* **Attribute name**  – a "camel" format representation of the database field, that can used on the GUI side \(javascript\) to refer the column or the model
* **To ignore with grid profile/permissions**  – flag used to activate or not the user profile and columns permissions for this column; it can come in handy to disable this feature for columns that could be visibile/hidden according to dinamic conditions
* **Position**  – column order in the grid
* **Header name**  – column title, that will be translated according to the language of the user; in case of an application having oneonly language, this property reports that real column header to show on grid
* **Column type**  – application type to apply for the column; typically this types are preset by the Web Designer when creating the grid and are compatible with the database field type; the user can change this application type and refine the column format, for instance by setting a column with a date type for a datetime field. Allowed application types are defined below
* **Code selector**  – in case the column has a combo-box/lookup type, this additional property must be defined, in order to specify which code selector will manage this column
* **Directory upload**  – in case the column has a "File upload/download" or "File path" or "Image path" type, this property must be defined, in order to specify which is the default directory where saving/loading files
* **Width**  – Field width
* **Field length**  – in case of text colums, this attribute defines the maximum characters allowed in edit
* **Integers number**  – in case of number column, this attribute defines the maximum number of integer digits allowed in edit
* **Decimals number**  – in case of number column, this attribute defines the maximum number of decimal digits allowed in edit
* **To uppercase**  – flag used to make the text edited by the user be in uppercase
* **Mandatory**  – flag used to force the editing of this column, which cannot be empty when saving data
* **Editable in insert mode**  – flag used to allow the editability of this column when the grid is in insert mode \(new rows\)
* **Editable in edit mode**  – flag used to allow the editability of this column when the grid is in edit mode
* **To hide**  – flag used to hide the column
* **Filterable**  – flag used to allow the viewing of the quick filter panel when right clicking with the mouse on that column, in order to apply a filtering condition on the grid
* **Exportable**  – flag used to make it possible to export data from the grid, including this column
* **Can copy**  – flag used to allow the copy of the cell value, when clicking on the copy button on the grid toolbar
* **Can sort**  – flag used to make it possible to order by this column, when clicking on the column header
* **Sort order**  – combo box having values "no sorting", "ascending", "descending", indicating if a column must be preordered when opening the grid; this property defines which will be the sorting versus
* **Sort position**  – this number represents the ordering position of this field in the ORDER BY clause generated on the server side, when ordering by this column; this property must be defined when "Sort order" property is set to "ascending" or "desceding"
* **Right padding**  – property used to apply the right padding to a text/char column: the number is used to ensure that the final value for the cell will have enough spaces on the right so that the final cell value will have a length equals to this number
* **To trim**  – flag used to apply a trim to the text \(no spaces on the left and right\)
* **To trim in filter**  – flag used to apply a trim to the text specified in the quick filter
* **Default value in insert mode**  – value to apply to the cell when the grid is in insert mode. You can choose a predefined variable, such as username or current date; as alternative, you can specify a variable having format :VARIABLENAME or a javascript expression, such as: record.data.attributeName
* **Default value in edit mode**  – value to apply to the cell when the grid is in edit mode
* **Positive value in check**  – Value saved for checked checkboxes \(e.g. ‘Y’\)
* **Negative value in check**  -Value saved for unchecked checkboxes /e.g. ‘N’\)
* **Currency symbol** 
* **Data format**  – format expressed in ExtJS compatible format, to use with numeric values; e.g. 0.000
* **Horizontal alignment**  – to the left/center/right
* **Minimum**   **date**  – in case of date/datetime type, it is possible to set a minimum date the user can set
* **Maximum date**  – in case of date/datetime type, it is possible to set a maximum date the user can set
* **Minimum numeric value**  – in case of number type, it is possible to set a minimum number the user can set
* **Maximum numeric value**  – in case of number type, it is possible to set a maximum number the user can set
* **Renderer**  – an optional javascript expression, to use to format data in a complex way; see ExtJS documentation about this property to know how to use it; 

Example for a Web Application:

```js
if (value&lt;0) return "negative"; if (value&gt;0) return "positive"; return "zero";
```

Example for a Mobile Application:

```js
var obj = { value: vo["COD_PRODOTTO"] }; 
if (vo["VALIDATO"]=="N") { 
  obj.backgroundColor = "FFDDDD";
} 
else { 
  obj.backgroundColor = "DDFFDD"; 
}; 
var val = convertToObjectJson(obj); 
return val;
```

* **Not editable if**  – boolean expression, expressed in javascript, indicating when the cells of the selected column are editable; this property overrides the default behavior of the cells, defined through the combination of grid mode \(insert/edit\) + can insert/can edit properties. This property is useful when the behavior of the cell should change according to a dynamic value, such as "a document state" represented by the value of another attribute of the same row.

Only for a  **pivot grid** , these are all the properties defined for a column:

* **Pivot column**  – flag used to set pivoting column
* **Grouping column**  – flag used to set column that is grouped value
* **Header column**  – flag used to set column header of grouped value

Allowed application types for columns, according to the related database field type:

| Database field type | Application type |
| :--- | :--- |
| Text | Text, Check-box, Local/Remote Combo-box, Button lookup, Code+Button lookup, File upload/download, Image Path, File Path, Button |
| Integer | Number |
| Decimal | Number |
| Char | Text, Check-box, Local/Remote Combo-box, Button lookup, Code+Button lookup |
| Datetime | Date, Datetime, Time |
| Date | Date, Datetime, Time |
| Internal Counter | Internal Counter |
| Counter based on a table | Counter based on a table |
| Counter based on a custom business component | Counter based on a custom business component |
| Sequence | Sequence |
| File identifier | File upload/download |

There is a difference between File upload/download, Image Path, File Path column types:  
 **File upload/download**  – an upload/download button is showed inside that column; through that button it is possible to show a dialog window used to download, upload, preview and delete a file; when uploading a file, this will be phisically stored in the server file system starting from the path specified through "directory upload" property in the grid columns designer; when saving, the uploaded file will be stored within the following subfolders structure:  
///filename.xxx  
That structure allows to store multiple versions of the file \(file versioning\).  
 **Image Path**  – this column type can be used to show a preview of the previously uploaded image; it cannot be used to upload or download imags; the images to show are retrieved starting from the path in the server file system starting from the path specified through "directory upload" property in the grid columns designer.  
 **File Path**  – an upload/download button is showed inside that column; through that button it is possible to show a dialog window used to download, upload, preview and delete a file; when uploading a file, this will be phisically stored in the server file system starting from the path specified through "directory upload" property in the grid columns designer; when saving, the uploaded file will be stored in that path.  
This column type does not allow to store multiple versions of the file.  
The  **Button**  type column allows to show a clickable button within a cell, for each cell of that column. It is then possible to attach a "cell click" event to it and consequently manage the binded action.  
The default behavior of that button is to show the cell value as its text, painted in white color on a blue background color. You can change the default behavior by setting the "renderer" property for that column, which has this default content:

```js
function(value, metaData, record, rowIndex, colIndex, store) {
    metaData.style = 'text-align: center;color: white; background: #3d71b8';
    return value
} // example for a Web Application
```

Note that it is not allowed to insert/delete columns in a grid: columns are automatically synchronized with the fields defined in the select clause of the binded business component, which are automatically synchronized with the data fields defined in the binded data model. The only exception to this rule is when the user is defining a business component "Query for a report to show on grid", where no data model is required: the select clause can be manually defined by the user and changes to this part of the SQL query are automatically reflected on the columns list of the linked grids.

---



