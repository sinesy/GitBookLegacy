# Filter properties

The filter controls list is an editable list where the user can refine the controls behavior. The default setting is automatically defined by the Web Designer, when creating the filter panel. During the filter panel definition, the select clause of the binded business component is analyzed: for each field in the select clause, a control is created and added to that list. Control type, linked label, mandatory, length are automatically set, according to the settings of the database fields: if a database field is mandatory, the control is mandatory and so forth.  
There are a great deal of filter control properties; in order to make it easy the filter control definition, not all properties are showed, only the most common; it is possible to access to the whole range of properties, by pressing the "Advanced mode" button on the toolbar.

These are all properties defined for a filter control:

* **To manage**  – flag used to define if the field must be managed, in terms of make it visible, editable and saved
* **Position**  – control order in the form
* **X**  – \(optional\) in alternative to the position, a label + control can be positioned exactly in a specific location, using x and y coordinates, expressed in pixels
* **Y**  – \(optional\) in alternative to the position, a label + control can be positioned exactly in a specific location, using x and y coordinates, expressed in pixels
* **Width**  – total width including label + control; note that for each controla label will be always created on its left, except when the label has a zero text length
* **Height**  – \(optional\) it can be useful in case of multi-line text controls
* **Label**  – text label, if it is empty, the label will be omitted
* **Operator**  – defines the filter operator to use: =, &lt;, &gt;, like, etc.
* **Control type**  – application type to apply for the control; typically this types are preset by the Web Designer when creating the form and are compatible with the database field type; the user can change this application type and refine the control format, for instance by setting a control with a date type for a datetime field. Allowed application types are defined below
* **Code selector**  – in case the control has a combo-box/lookup type, this additional property must be defined, in order to specify which code selector will manage this control
* **Directory upload**  – in case the control has a "File upload/download" type, this property must be defined, in order to specify which is the default directory where saving/loading files
* **Default value**  – value to preset into the filter control
* **Field length**  – in case of text controls, this attribute defines the maximum characters allowed in edit
* **Integers number**  – in case of number control, this attribute defines the maximum number of integer digits allowed in edit
* **Decimals number**  – in case of number control, this attribute defines the maximum number of decimal digits allowed in edit
* **To uppercase**  – flag used to make the text edited by the user be in uppercase
* **Mandatory**  – flag used to force the editing of this control, which cannot be empty when saving data
* **Can copy**  – flag used to allow the copy of the control value, when clicking on the copy button on the form toolbar
* **Right padding**  – property used to apply the right padding to a text/char control: the number is used to ensure that the final value for the control will have enough spaces on the right so that the final control value will have a length equals to this number
* **To trim**  – flag used to apply a trim to the text \(no spaces on the left and right\)
* **Positive value in check-box control** 
* **Negative value in check-box control** 
* **Minimum date**  – in case of date/datetime type, it is possible to set a minimum date the user can set
* **Maximum date**  – in case of date/datetime type, it is possible to set a maximum date the user can set
* **Minimum numeric value**  – in case of number type, it is possible to set a minimum number the user can set
* **Maximum numeric value**  – in case of number type, it is possible to set a maximum number the user can set.

Allowed application types for controls, according to the related database field type:

| Database field type | Application type |
| :--- | :--- |
| Text | Text, Multi-line text, Check-box, Local/Remote Combo-box, Button lookup, Code+Button lookup |
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

Note that it is not allowed to insert/delete filter controls in this list: filter controls are automatically synchronized with the fields defined in the select clause of the binded business component, which are automatically synchronized with the data fields defined in the binded data model.

---



