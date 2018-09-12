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
* **Parameters filler** - it is likely that many SQL extraction queries \(see next section "Extract data from"\) can contain variables, expressed as :VARNAME. In case of parameters such these ones, it is required to specify the parameters values when executing an export task. An export task can be started manually or automatically. In case of a manual execution, the end user can select a task definition from the tasks list \(see previous section\) and press the "**Execute export**" button. Here the user will be prompt with an input dialog where he has to specify all parameters values, so that the execution process can work properly. As an alternative, an export process can be started automatically, using the Scheduler. In such a scenario, the parameters values must be provided automatically: 



**Copy to folder **- it is optional and can be filled out, in case the exported files must be saved on a directory \(server file system, Google cloud\)

**Copy to FTP** - it is optional and can be filled out, in case the exported files must be moved to a virtual folder within an FTP server



### Extract data from

gg













