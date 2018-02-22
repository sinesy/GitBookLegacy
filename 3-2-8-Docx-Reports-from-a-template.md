# Docx templating

4WS.Platform provides a feature to create docx documents on the fly, starting from a docx template. The template can contain images, paragraphs, tables or any other kind of object; it can also contain special tags that will be replaced by values by Platform, when the template is executed to produce the final docx. Values to fill in come from a main query or from a subquery, linked to a report table.  
Through the App Designer it is possible to define a list of reports and for each of them a set of docx template, one for each supported language. In this way when launching a report, Platform will use the template related to the current language.  
When uploading a template, the App Designer will analyze the docx content, searching for the "special tags" and subreports \(i.e. tables\). These are the supported tags:

* **&lt;table&gt;**
* **&lt;td&gt;**
* **&lt;tdtranslation&gt;**
* **&lt;control&gt;**
* **&lt;translation&gt;**
* **&lt;subform&gt;**
* **&lt;subcontrol&gt;**
* **&lt;subcontroltranslation&gt;** 

For each tag belonging to the main report \(control or translation\), a corresponding field will be created and linked to the report definition: when configuring the report, a value must be mapped to each of these fields, in order to provide a value to fill in for each of them.  
Values to link to each field can be:

* a field in the select clause of the main query \(in case of a main report field\)
* you can map that field to a tag
* you can map the prefix of a field in the select clause to a tag, in case of translations not stored in a dictionary table but to a series of fields, one for each language; so if you have a table mapped to the select clause having a set of fields for each language, here you have to map the prefix common to al these fields.
  For example, if you have a table with fields: DESCRIPTION\_IT, DESCRIPTION\_EN, DESCRIPTION\_DE defined in the select clause, you can map a tag to DESCRIPTION; in this way, the report generator will automatically choose the DESCRIPTION\_xx field, according to the current language, that is to say, xx will be the value of the current language.
* a field in the select clause of a subquery \(in case of a subreport field – aka table\)
* a constant
* a system variable, such as :TODAY, :USERNAME, etc
* a predefined function with its argument values; supported functions are:
* INCREMENT\_DATE\(NUMBEROFDAYS\) – creates a date, starting from the current day, incremented by a number of days specified as the first argument
* PROGRESSIVE\(TABLENAME,COLNAME\) – generates an internal counter, incremented by 10, using CON09\_PROGRESSIVES table, where there is a record for each counter, whose primary key is composed of tablename and columname
* COUNTER\(TABLENAME,VALUECOLNANE,INCREMENTVALUE,WHERE\) – generates a generic counter, incremented by the specified value, using an external table, provided by the user, where a single record can be identified throught the specified where clause \(the word WHERE must NOT be included\); the table name and the column name containing the current value must be specified too.

### Example

COUNTER\(DOC\_COUNTERS,CURR\_VALUE,1,DOC\_TYPE=’SELLORD’ and  
YEAR=2014\)

Supported system variables are the same used in the rest of Platform.  
The report definition requires the following data:

* report description
* a set of .docx templates, one for each language
* a mapping for each field of the main report
* a mapping for each table cell of the subreport

Independently of the field, additional settings can be defined:

* format – the format to use for a date/number field;
* in case of date, the format is expressed according to the Java Format for Date \(e.g. yyyy-MM-dd\); if not specified, the default date format defined for current language will be used
* in case of a number, the format is expressed according to the Java Format for Number; if not specified, the default number format defined for current language will be used
* renderer – a javascript program, used to define the result string to show for the current value; that program can contain any number of js commands and has as input the "vo" variable containing the couples , for each value of the main query.

The program must terminate by returning the result string to show, through the command: utils.setReturnValue\(valueToReturn\);

### Example

```js
var showDecimals = false;

var decimals = 2;

var langId = userInfo.languageId;

var text = utils.numberToText(vo.number,decimals,langId,showDecimals,’/’);

utils.setReturnValue(text);
```

---



