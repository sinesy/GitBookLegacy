# Data Export

This functionality allows to export a list of data stored in a database and save it as a file.

The data list comes from

* a specific database **table**, optionally filtered by a custom filter condition
* a more general **SQL query**, which can extract data coming from a variety of different tables; again, a filtered condition can be specified

Exported data formats are:

* **csv**, with comma o semi-colon
* **4WS.Trade data export format** \(a sort of csv\)
* **SQL insert instructions**, whose syntax depends on the selected target database

It is possible to set variables in the filtering conditions, so that the real values are specified at execution time.

Moreover, a group of export tasks can be defined, so that each export task in the same group is executed according to a specific order. The goal of a group is to create a .zip file containing all export data files belonging to the same group, instead of multiple files; this format is particularly helpful to be sent over the Internet, for instance via email or FTP or whatever.

It is possible to specify the final destination of the generated files:

* a directory defined through the App Designer, so that the file can be stored on the server file system or on the Google Cloud \(Cloud Storage, Drive, etc\)
* on a virtual folder within an FTP server

Finally, it is possible to automate data export through the embedded Scheduler available in the App Designer, by choosing the export type:

* export a single job
* export a group of jobs
* export all jobs

In the second and third case, the execution order for the jobs is the one defined at job level.

### Data export list

The definition of a task starts from the **Table Export** menu item, within the **Services** menu of the App Designer.

Table Export functionalities shows all tasks defined until now.

![](/assets/export_lista.png)

Here defined tasks are reported ordered by the export order, defined at task level.

The order is used when automating the export for all tasks or for a group of tasks.

When pressing the Add button, it is possible to create a new export definition. When double clicking on an already existing row or pressing the Detail button, it is possible to review an already existing task and edit it.

A task definition is split up in a sequence of panels, composing a wizard, which drives the user along the definition process.

![](/assets/export_def.png)

### Data export definition

The first step involves the definition of the export format and destination, through the **Export definition** panel, organized in 3 sections:

**Settings** - contains the main settings for the job

It includes the following input fields:

* **Description** - described the jon
* **Enabled** - flag used to ignore the job execution within an automated export performed by the Scheduler, in case of export of a set of jobs \(export of a group or export all\)
* **Delete content** - not managed at the moment
* **Export type** - allows to define the export format: CSV, 4WS.Trade data format, SQL insert instructions
* Target database type - optional; used in case of SQL export type: it define the destination database type \(e.g. Oracle, SQL Server\), in order to generate SQL instructions compatible with the selected database type
* **File name** - export file name
* **File name policy **- optional value; if specified, the file name is ignored \(except for the file extension, e.g. .csv, .txt\) and the real file name will be the one defined here; it supports a dynamic name definition. Examples: yyyy-MM-dd_HH-mm-ss or 'FILE_'yyyy-MM-dd_HH-mm-ss_
* **Group name** - optional: if specified, it means the current task will be part of a group of jobs sharing the same group name; none of them will be moved to the specified destination
* **Group zip file name **- it must be used together with the "group name" field; if specified, at the end of the current job export task, all files already exported will be compressed together in the same .zip file, whose name is the one specified here; that means that _**only the last task in the group should have this field filled**_, since only at the end of all export tasks, a .zip file should be generated!
* **Group file name policy **- optional value; if specified, the .zip file name is ignored and the real file name will be the one defined here; it supports a dynamic name definition. Examples: yyyy-MM-dd_HH-mm-ss or 'FILE_'yyyy-MM-dd_HH-mm-ss_
* **Export order** - this field defines the execution order for a set of jobs; it is used only by the Scheduler to figure out the execution order, in case of "export of a group" or "export all" option
* **Action before export **- server-side javascript action which can be optionally executed before starting the execution process
* **Action after export **- server-side javascript action which can be optionally executed after the execution process
* **Parameters filler** - it is likely that many SQL extraction queries \(see next section "Extract data from"\) can contain variables, expressed as :VARNAME. In case of parameters such these ones, it is required to specify the parameters values when executing an export task. An export task can be started manually or automatically. 
  * In case of a manual execution, the end user can select a task definition from the tasks list \(see previous section\) and press the "**Execute export**" button. Here the user will be prompt with an input dialog where he has to specify all parameters values, so that the execution process can work properly. 
  * As an alternative, an export process can be started automatically, using the Scheduler. In such a scenario, the parameter values must be provided automatically: for that reason, a business component for a list can be set in "Parameter filler" field. This business component must contain in the SELECT clause all required parameter names. When executing the task, first the business component will be executed and the list of parameter values are retrieved; then for each record read, the job is executed, so that it is possible to automate the job execution multiple time, once for each record read from the business component.

 

**Copy to folder **- it is optional and can be filled out, in case the exported files must be saved on a directory \(server file system, Google cloud\)



**Copy to FTP** - it is optional and can be filled out, in case the exported files must be moved to a virtual folder within an FTP server.

The FTP virtual folder can be defined dinamically, by including supported Platform variables.

For example, a valid folder definition can be:

LISTINO\_:ENTE\_:FILIALE



### Extract data from

The second step in the job definition is related to the data extraction query.

![](/assets/export_query.png)

This SQL query can be defined in 2 ways:

* by specifying a table: in that case, a filtering condition can be defined, including bind variables
* by choosing a generic SQL query: in that case, the query is not limited to a single table, but can include any number of tables connected by JOIN conditions; again, it can include bind variables.

When pressing the next button, the query is automatically tested: in case of invalid syntax, the error is prompted to the user, who has to fix the incorrect syntax before continuing.

Another prompt is always shown to the user at this state: whether updating output fields. For each field specified in the SELECT clause, an output field is defined by Platform and automatically mapped to the corresponding SELECT field. In the section named "**Output** **Fields**", the end user has the change to set additional data conversion on the output field, like its type or date conversion mask.



### Additional SQL queries or statements

In the previous step, the user must specify the main query, i.e. the extraction query to execute. 

![](/assets/export_otherqueries.png)

Here it is possible to specify 

* an additional query, named "Query executed with an empty db" can be defined; it will be used when \(i\) manually starting the task and the user has chosen such an option when prompted or \(ii\) when automatically starting the task by the Scheduler and the Scheduler parameter named "QUERY\_TYPE" has been specified and set to "I"
* SQL statements executed before or after the query for empty db
* SQL statements executed before or after the standard query

The last two options will be automatically executed by Platform, without any prompt to the user.



### Output fields

This step allows the user to change a few settings related to the output fields: these are automatically defined by Platform, starting from the main query defined at step 2.

![](/assets/export_fields.png)

If needed, the user can change the target field type or its format, for instance in case of a date type, when it must be converted to a text having a specific format. If not specified, a date type input field is automatically converted to a text value having format "yyyy-MM-dd HH:mm:ss"

The order property plays a very important role: it represents the order inside a CSV used to fill in the values for the fields. As a default behavior, fields are reported with the same order reported in the SELECT clause, so an easy and quick way to define the output order for values, is simply reporting them in the SELECT clause according to the desired sequence.



### Query parameters

This is the last step in the export task definition: it reports all bind variables found in the SQL extract query.

![](/assets/export_params.png)

The use has the chance to specify here the values for all or part of them.

All missing values will be prompted when manually executing a data export \(see first section\).

In case the export is automatically started by the Scheduler, all required values must be specified either as Scheduler parameters or through the **Parameters filler** described in the first step. 

If there are bind variables not filled, the export process will fail with an error.



### Scheduling data export

Platform Scheduler includes 3 alternative ways to automate the data export execution.

![](/assets/export_sched.png)

**Export single job** - The first option is executing a single data export: in this case, you have also to specify which job to execute, through the "Command to run" field, which is filtered by all defined jobs.

**Export a group** - This option will automate the execution of all jobs belonging to the same group: jobs are executed in the order defined though the"Execution order" field specified for each job. You have also to specify which group to execute, through the "Command to run" field, which is filtered by all defined groups.

**Export all** - This option will automate the execution of all jobs: jobs are executed in the order defined though the"Execution order" field specified for each job. 



Bind variables are filled according to the following policy:

* values coming from the "Parameters" folder \(last step of job definition\)
* values defined though the Scheduler parameters
* values coming from the execution of the SQL query included in the Parameter Filler component





### 

### 







