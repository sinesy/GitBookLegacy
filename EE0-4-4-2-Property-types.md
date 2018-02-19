# Property notes

Five different types of properties are supported in Activiti:

* string
* long
* date
* enum
* boolean

**String**   
Text-field used to store any alphanumeric value

**Long**   
Text-field used to store any numeric \(integer or decimal\) value

**Date**   
Text-field used to store a date/date+time value  
In case the date must be formatted with a specific format \(e.g. day-month-year rather than month-year-day\), a utility method can be used to format it:  **utils.formatDate\(…\)**   
This is helpful for instance when a date must be included the body of an email message or in the "documentation" property of a task.

### Example

${utils.formatDate\(DATE\_VARIABLE\)}

or

${utils.formatDate\(DATE\_VARIABLE,’dd-MM-yyyy’\)}

**Enum**   
An enumeration is a static list of values, feasible to feed a combo-box.  
The grid available in the bottom part of the property definition dialog can be used to set this list of values. Both ID and NAME are required.

**Boolean**   
A Check-box field used to set a "true" or "false" value when selecting/deselecting it.

---



