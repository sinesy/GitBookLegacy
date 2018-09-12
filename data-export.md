# Data Export



This functionality allows to export a list of data stored in a database and save it as a file.

The data list comes from

*  a specific database **table**, optionally filtered by a custom filter condition
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





### Data export definition

The definition of a task starts from the **Table Export** menu item, within the **Services** menu of the App Designer.

Table Export functionalities shows all tasks defined until now.

![](/assets/export_lista.png)

Here defined tasks are reported ordered by the export order, defined at task level.

The order is used when automating the export for all tasks or for a group of tasks.









