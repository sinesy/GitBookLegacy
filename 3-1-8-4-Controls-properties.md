# Controls properties

The controls list is an editable list where the user can refine the controls behavior. The default setting is automatically defined by the Web Designer, when creating the form. During the form definition, the select clause of the binded business component is analyzed: for each field in the select clause, a control is created and added to that list. Control type, linked label, mandatory, length, editability in insert/edit modes are automatically set, according to the settings of the database fields: if a database field is mandatory, the control is mandatory, if a database field is part of a primary key, the related control is not editable in edit, and so forth.  
There are a great deal of control properties; in order to make it easy the control definition, not all properties are showed, only the most common; it is possible to access to the whole range of properties, by pressing the "Advanced mode" button on the toolbar.

![](http://4wsplatform.org/wp-content/uploads/2015/12/detailDetail-1024x518.jpg)

These are all properties defined for a control:

* **To manage**  – flag used to define if the field must be managed, in terms of make it visible, editable and saved
* **To show**  – flag used to define if the control is visible; even if it is declared as not visible, the user can always make it visible when interpreting the application, by switching that settings with right click of the mouse on the control header
* **Position**  – control order in the form
* **X**  – \(optional\) in alternative to the position, a label + control can be positioned exactly in a specific location, using x and y coordinates, expressed in pixels
* **Y**  – \(optional\) in alternative to the position, a label + control can be positioned exactly in a specific location, using x and y coordinates, expressed in pixels
* **Subpanel title**  – \(optional\) if specified, a sub panel will be created inside the form container using this title and including inside it any label + control having this subpanel title; this property makes it possible to group labels/controls in several panels within the form
* **Subtab title**  – \(optional\) if specified, a sub tab will be created inside the form container using this title and including inside it any label + control having this subpanel title; this property makes it possible to group labels/controls in several tabbed panes, within the form; tab panes and sub panes can be combined too
* **Width**  – total width including label + control; note that for each controla label will be always created on its left, except when the label has a zero text length
* **Height**  – \(optional\) it can be useful in case of multi-line text controls
* **Label**  – text label, if it is empty, the label will be omitted
* **Control type**  – application type to apply for the control; typically this types are preset by the Web Designer when creating the form and are compatible with the database field type; the user can change this application type and refine the control format, for instance by setting a control with a date type for a datetime field. Allowed application types are defined below
* **Code selector**  – in case the control has a combo-box/lookup type, this additional property must be defined, in order to specify which code selector will manage this control
* **Directory upload**  – in case the control has a "File upload/download", "File path" or "Image path" type, this property must be defined, in order to specify which is the default directory where saving/loading files
* **Field length**  – in case of text controls, this attribute defines the maximum characters allowed in edit
* **Integers number**  – in case of number control, this attribute defines the maximum number of integer digits allowed in edit
* **Decimals number**  – in case of number control, this attribute defines the maximum number of decimal digits allowed in edit
* **To uppercase**  – flag used to make the text edited by the user be in uppercase
* **Mandatory**  – flag used to force the editing of this control, which cannot be empty when saving data
* **Editable in insert mode**  – flag used to allow the editability of this control when the form is in insert mode
* **Editable in edit mode**  – flag used to allow the editability of this control when the form is in edit mode
* **Can copy**  – flag used to allow the copy of the control value, when clicking on the copy button on the form toolbar
* **Right padding**  – property used to apply the right padding to a text/char control: the number is used to ensure that the final value for the control will have enough spaces on the right so that the final control value will have a length equals to this number
* **To trim**  – flag used to apply a trim to the text \(no spaces on the left and right\)
* **Default value in insert mode**  – value to apply to the cell when the form is in insert mode. You can choose a predefined variable, such as username or current date; as alternative, you can specify a variable having format :VARIABLENAME or a text, such as abc, which will be then automatically surrounded by ‘ ‘: ‘abc’; as alternative, you can also specify a javascript expression, such as: ‘+record.data.attributeName+’ \(Pay attention to the use of ‘  and ‘ before and after the javascript expression: that depends on the fact that in detail forms a string is required and it is then surrounded by ‘ ‘, so you have to add ‘  and  ‘ to close the string and concatenate something other: ”+record.data.attributeName+”\)
* **Default value in edit mode**  – value to apply to the cell when the form is in edit mode
* **Positive value in check**  – Value saved for checked checkboxes
* **Negative value in check**  -Value saved for unchecked checkboxes
* **Currency symbol** 
* **Data format**  – format expressed in ExtJS compatible format, to use with numeric values; e.g. 0.000
* **Minimum date**  – in case of date/datetime type, it is possible to set a minimum date the user can set
* **Maximum date**  – in case of date/datetime type, it is possible to set a maximum date the user can set
* **Minimum numeric value**  – in case of number type, it is possible to set a minimum number the user can set
* **Maximum numeric value**  – in case of number type, it is possible to set a maximum number the user can set
* **Not editable if**  – boolean expression, expressed in javascript, indicating when the control is editable; this property overrides the default behavior of the control, defined through the combination of the form mode \(insert/edit\) + can insert/can edit properties. The property is useful when the behavior of the control should change according to a dynamic value, such as "a document state" represented by the value of another attribute of the same record.
* **Icon name**  – in case of button type, it is possible to select an icon.

Allowed application types for controls, according to the related database field type:

| Database field type | Application type |
| :--- | :--- |
| Text | Text, Multi-line text, Check-box, Local/Remote Combo-box, Button lookup, Code+Button lookup, Image combo "File upload/download", "Image Path", "File Path", Button, Label |
| Integer | Number |
| Decimal | Number |
| Char | Text, Check-box, Local/Remote Combo-box, Button lookup, Code+Button lookup, Button, Label |
| Datetime | Date, Datetime, Time |
| Date | Date, Datetime, Time |
| Internal Counter | Internal Counter |
| Counter based on a table | Counter based on a table |
| Counter based on a custom business component | Counter based on a custom business component |
| Sequence | Sequence |
| File identifier | File upload/download |

There is a difference between File upload/download, Image Path, File Path control types:  
 **File upload/download**  – an upload/download button is showed as graphics control; through that button it is possible to show a dialog window used to download, upload, preview and delete a file; when uploading a file, this will be phisically stored in the server file system starting from the path specified through "directory upload" property in the form controls designer; when saving, the uploaded file will be stored within the following subfolders structure:  
///filename.xxx  
That structure allows to store multiple versions of the file \(file versioning\).  
 **Image Path**  – this control type does not show a preview of the image, as for the grid it works exactly as the "File path" control type.  
 **File Path**  – an upload/download button is showed inside that column; through that button it is possible to show a dialog window used to download, upload, preview and delete a file; when uploading a file, this will be phisically stored in the server file system starting from the path specified through "directory upload" property in the form controls designer; when saving, the uploaded file will be stored in that path.  
This column type does not allow to store multiple versions of the file.  
Note that  **if you need to show a preview of an image in a detail window** , you should follow these steps:

* create a window containing a form panel, through the windows wizard feature of the web designer
* add an "Image Panel" to that window, so that the window would contain the form panel in the north and the image panel in the center of the window
* create an "after loading" event linked to the form panel, used to force the loading of the image in the image panel named loadImagePanelXXX, each time the form panel is loaded; a javascript action should be linked to that event containing the following instruction:

```js
loadImagePanelXXX(vo);
```

Note that it is allowed to insert/delete "virtual" controls in this list for added controls to form. This controls are not saved.  
Not "virtual" controls are automatically synchronized with the fields defined in the select clause of the binded business component, which are automatically synchronized with the data fields defined in the binded data model.

---



