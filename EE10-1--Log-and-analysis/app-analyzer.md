## App analyzer

This feature analyzes the app behavior, from different perspectives, including queues and scheduled processes performance, resources consumption, grave misconfigurations, user sessions and threads, etc.

The aim of this functionality is to provide a snapshot of the current status of the application, as well as monitoring automatically the behavior of the application over time.

Consequently, you can use it manually, by accessing this panel or let the system work alone.

You can use the global parameter APP\_ANALYSIS -&gt;**Enable application analysis every X hours **to set how much time to wait before the analysis is automatically carried out. This wait time is expressed in hours. If not specified, the app analysis is disabled.

The settings panel allows you to set the right settings to monitor and decide for each, which are the trigger values to take into account and the action to carry out when the tigger is fired.

For example, it is possible to monitor the CPU rate and set a trigger of &gt; 90% consumption: when this value is overpassed, an action is executed.

Supported actions are:

* log the event on the **Log table**, so that you can see it later, through the Log table functionality \(see that section for more details\)
* log the event on the **Log file**, so that you can see it later, through the Application Log functionality \(see that section for more details\)
* send an email to a list of addresses. In order to send notifications by email, you have first to define a few global parameters, needed to correctly configure the connection with an SMTP server:
  * MAIL -&gt; **SMTP host when sending email **+ all other SMTP xxx properties
  * APP\_ANALYSIS -&gt; **Email used to send notifications after an app analysis**; you can specified a comma \(,\) separated list of email addresses
  * APP\_ANALYSIS -&gt; **Subject to use in SMS/email after an app analysys**
* send an SMS to a list of phone numbers. In order to send notifications by SMS, you have first to define a few global parameters, needed to correctly configure the connection to Twilio SMS gateway, the service Platform uses to send SMS messages:
  * SMS -&gt; **Twilio SMS Account SID**
  * SMS -&gt; **Twilio SMS Auth Token**
  * SMS -&gt; **From SMS Phone Nr**
  * APP\_ANALYSIS -&gt; **Destination Phone Nr. when sending SMSs after an app analysis**; you can specified a comma \(,\) separated list of phone numbers
  * APP\_ANALYSIS -&gt; **Subject to use in SMS/email after an app analysis**



[![](http://4wsplatform.org/wp-content/uploads/2018/01/Schermata-2018-01-22-alle-08.41.46.png)](http://4wsplatform.org/wp-content/uploads/2018/01/Schermata-2018-01-22-alle-08.41.46.png)



You can analyze a wide range of variables related to your applications. They are grouped in 3 main areas:

* **Severe **– these are resources particularly important to monitor, since they could lead to the collapse of the whole system. Consequently, it could be helpful to enable a notification action like an email or SMS.
* **Warning **– these are resources that typically do not lead to a blocking condition, but they could become critical if ignored on the long time.
* **Configuration **– in this group are reported a series of misconfigurations which should be fixed by the developers who configured the application

Each resource to analyze has a threshold: when this is overpassed, the corresponding action is carried out. For a few resources, two thresholds are provided, one expressed as an numeric value, the other as a percentage.

The complete list of resources under analysis is as follow:

#### **Severe resources**

* **Empty file system **– analyze how much free space there is still in the server file system and in any other file system referred by the Directories set. The thresholds for this resource are expressed as follows:
  * when &lt; 500 MBytes, fire the action or
  * when &lt; 5% of the total space, fire the action
* **Free heap memory **– analyze the free Heap memory, available for the application execution. For example, the memory could be reduced dramatically because of the execution of queries retrieving an excessing number of records or when there are too many server-side actions under execution or too many user sessions.
  The threshold is expressed in percentage: when &lt; 5% of the total heap memory, the corresponding action is carried out.
* **Too many sessions **– analyze how many user sessions are active at the moment. An excessive number of sessions could be generated in case of stateful web services whose sessions has never been closed. 
  The threshold is expressed as the number of sessions: when &gt; 100 sessions, fire the action
* **Too many db connections **– analyze the current number of opened database connections. When &gt; 90, fire the action
* **Errors when opening db connections **– look for errors when opening a database connection; these errors could rise when a too large number of database connections has been created and the pooler/database is not able to provide additional connections. When more than 5 errors have been found, fire the action. 
* **High CPU rate **– analyze the CPU consumption. When &gt; 90%, fire the action



#### **Warning condition**

* **Too many threads **– analyze the number of threads; an excessive number of threads could lead to an high consumption of memory and it could depend on too many server-side javascript actions under execution or too many concurrent HTTP requests. When &gt; 25 thread, the corresponding action is carried out.
* **Additional datastore **– fire the action when &gt; 2 datastores configured
* **Records in log table **– fire the action when there are more than 1.000.000 records stored
* **Too many queues **– fire the action when there are more than 100 queues defined
* **Too many elements in queue **– fire the action when there are more than 1000 elements in a queue
* **Requests API discarded **– fire the action when there are more than 10 errors for requests discarded
* **Slow requests **– fire the action when HTTP requests last more than 30 seconds
* **Invalid credentials **– fire the action when there are more than 10 errors due to invalid credentials; maybe a brute force attack?
* **Requests at second **– fire the action when there are more than 10 HTTP requests per second
* **\[Mobile\] Synchronizations slower than **– fire the action when a synchronization process between the server and a mobile device lasted more than 30 seconds
* **\[Mobile\] Registered devices **– fire the action when there are &gt; 1000 registered devices
* **\[Mobile\] Context path size **– fire the action when the context path contains files which consume more than 1 MByte
* **\[Mobile\] Synchronization folder size **– fire the action when the temporary space on the server used to store files for the mobile devices is using more than 10 GBytes
* **\[Mobile\] Slow batch data distribution **– fire the action when the internal process used to prepare data for all mobile devices is lasting more than 1 minute.



#### **Misconfiguration**

* **Nr of records to check when executing queries **– fire the action when a SQL query is giving back more than 100 records; this is never a good idea: it leads to a dangerous consumption of memory. Query should always be configured to get a page of data and the page size should be limited to 30-50 records.
* **Found errors when executing actions **– when errors have been found on the execution of server-side javascript actions, the corresponding action is executed if there are more than 100 errors
* **APIs using auth token never closed **– fire the action when at least 5 invocations of a restful web service have been found and for them no close session method has been called. This is a very important event to take into account, because on the long term it could lead to a high consumption of memory and to the collapse of the server
* **Max execution time for queries **– fire the action when there is a SQL query lasting more than 3 seconds
* **Max execution time for queries COUNT\(\*\)**– a grid is usually linked to a business component whose purpose is to collect data used to fill in the grid. Data is retrieved through a couple of SQL queries: the first is the main query, whose result represent the content of the grid; the second query is a SELECT COUNT\(\*\) query, used to reckon the total amount of records that are potentially available for the grid. This second query could last too much time, especially in case of a database table particularly large. This threshold is related to the second query time: the corresponding action is executed if the second query lasts more than 3 seconds
* **Scheduled processes too frequent**– fire the action when a \(not suspended\) scheduled process has a scheduling time less or equal to 5 minute. This is not necessarelly a bad thing: it depends on how complex the batch executed in such a time is.



When pressing the **Analyze **button, the analysys is performed and the outcome is reported in the Results subfolder.

Example of analysis outcome:

[![](http://4wsplatform.org/wp-content/uploads/2018/01/analize-1024x547.png)](http://4wsplatform.org/wp-content/uploads/2018/01/analize.png)

**Note**: the thresholds set in the first panel, after pressing the Analyze button, are stored by Platform and used in every subsequent analysis, both manual and automatic. That means you can change the threshold values, press the Analyze button and at regular intervals, Platform will perform the analysis using those values, since they are not only used for the manual analysis but also for the automated ones.

**Note**: there are a few checkings which are carried out independently of what set on the Settings folder, since they do not require an input value for executing the checking:

* Invalid additional datasources, for example for a database connection not set correctly
* Definition of HTTP request aliases which do not have a removeSession=true parameter and do not have a logoutApp subsequent request
* Out of memory errors
* Scheduled processes which are running for a too long time, so long that is greater than the wait scheduled time \(e.g. a process scheduled every 5 mins, whose execution is longer than 5 mins\)
* Database connections locking



