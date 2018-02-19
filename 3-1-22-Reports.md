4WS.Platform includes Jasper Report version 4.5.1. You can develop report templates using for instance iReport free designer. Together with .js and .class custom files, you can also include report templates.
Once included in the custom application subfolder, these will become available to the Web Interpreter. A report can be invoked:
as a menu item from the application menu
as a button in a panel; in this case, you can also pass parameters to the report.
Using "Application Menu" menu item you can define folders and menu items, including reports.
In any case, a wizard is prompted in order to define all information required by the report.
Reports have to be included in the subfolder of the specific application (e.g. /tomcatxxx/webapps/platform/yourapplicationsubfolder/report1.jasper).
Once selected a report template in the wizard, the list of parameters is reloaded after analyzing the report template and all required parameters are reported. In this way it is possibile to define how each parameter should be managed.

![](http://4wsplatform.org/wp-content/uploads/2015/12/newReport-1024x522.jpg)

Required data to specify when defining a report execution are:

*  **text**  to show in the menu item or text button, used to execute the report
*  **report name** , fetched from the list of .jasper files stored within the subfolder in the Platform web context
*  **datastore**  to use when invoking the report, that is to way, the database connection to pass to the report in order to allow the report to retrieve data from a database on its own
*  **report format ** &#8211; PDF or XLS
*  **list component**  &#8211; optional field; it can be used if the report must be filled in with a list of records expressed in JSON format and coming from a business component; the requirement is that the business component must provide a list of records, not a detail business component.

Additional requirements to meet on the iReport side are:

* the query to set must remain empty BUT the query language MUST be set to JSON
* declared fields must respect the naming of the JSON response, i.e. fields must be attributes (e.g. itemCode, description, etc.); moreover,  **the "description" property of each field must be filled to, with the same attribute name** , otherwise the resulting report will not contain any result (null values instead of the real values provided by the JSON response).

For each parameter it is possible to include it in the filter panel or not.
Each parameter can be managed in 4 alternative ways:

* without any preset value, typically for parameters to show in the filter panel and to fill in by the user on the fly
* with a constant value, typically for parameters to preset and not to show in the filter panel
* with a variable (expressed as :XXX), dynamically set when opening the report, typically for parameters to preset and not to show in the filter panel
* with a code selector, to show in the filter panel and to fill in by the user by choosing a value from the list proposed in the codes list (lookup, combobox, etc.)

In case at least one parameter has been configured to be viewed, a filter panel is proposed each time the user press on the report: in this ways the user can set the values in the filter controls and then generate the report. In case no parameters have been defined to be showed, the report is directly generated when pressing on the report generation (i.e. menu item or report button in grid/form).

 **Filling a Jasper Report template with a server-side js business component** 
You can use iReport to create a report template which is not connected to a SQL query, but it is fill with a list of records expressed as a JSON string, passed by Platform to the report, when executing it.
The steps to follow are:

* create a report template with iReport, without specifying a SQL query
* choose &#8220;Use the report JSON Expression when filling the report&#8221; to be able to specify your query within the individual report
* in iReport&#8217;s &#8220;language query&#8221;, choose  **JSON**  in the drop-down
* in iReport&#8217;s &#8220;text query&#8221;,  **set the attribute**  in JSON containing the list of data (e.g. valueObjectList)
* define manually every field needed in the report (see the section &#8220;Fields&#8221;), by pressing the &#8220;Add&#8221; button to add the field; here it is essential to set also the &#8220;description&#8221; field and not only the field name: the &#8220;description&#8221; field must be set with the attribute name reported in the JSON list of data
* it is not possible to test the report directly from iReport: you have to publish it into Platform
* during the publishing process of the report in platform, you have to fill also the &#8220;List component&#8221; optional lookup: here you have to choose the right business component, which has to provide the same attributes you defined in the report template

                

---


