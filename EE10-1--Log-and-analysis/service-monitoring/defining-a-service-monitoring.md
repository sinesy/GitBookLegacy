# **Defining a service to monitor**

**        
**The App Designer menu-bar provides the “**Monitoring Services” -&gt;“Monitoring services**” submenu through which it is possible to define any number of services to track.

---

![](https://lh5.googleusercontent.com/rN4424PTxWdB9jxbqeYIAGzWW3JxM8vhwyT9RCZFumFV0da4FQqHWoL7cPgbOKzKGd_SlzriTfZxL7P942Hr4vj8StFV5bFzstUgeKSkTiCa2Rf_SNHW6Hs5HDgjkNdo6IyLTrmx)

**        
**

This is the list containing all defined services under monitoring.

Through it, any number of services can be configured, through the Add button.

** **![](/assets/Schermata 2020-02-24 alle 12.02.36.png)

The detail window requires the following fields:

* **\(service\) code** - this is a mnemonic value you can use later, when searching for log; it can be helpful to reuse the same service code along multiple Platform installations, so that the same cross-server functionality can be monitored, starting from the same code

* **description** - a multi-language description; according to the logged user, a different description can be reported, expressed in the user language; when saving for the first time a service, all descriptions for all languages are saved with the same content, the one defined in this field; it is possible to change description according to the language, by clicking onInternationalization -&gt; Translations;when saving this window in update mode, only description for the current user language is updated, not the descriptions for other languages

* **type** - this represents the type of service to monitor; supported services are: server-side javascript actions, export data from table; according to the service type, the “Command” input field changes and show a different input control, in order to select an action or an export job configuration

* **command** - the service to monitor \(e.g action, export job, etc.\); at the moment, only the ones reported above are supported; it means that web services, enqueued actions, actions, scheduled actions, single data export job, a group of export jobs are all supported.

* **enabled **- flag defining whether the current service must be monitored or not; this flag is helpful to temporary disable the monitoring of services

* **storage log **- log messages are not stored forever: through this field it is possible to define the maximum amount of logged messages to store, expressed in days; all messages older than this value are automatically deleted \(once a day\)

* **log level **- when a service is under monitoring, each elaboration is automatically saved \(in terms of start/end datetime, execution state, I/O\); optionally it is possible to append additional log messages for a single elaboration; this messages can be logged or not, according to the log level; Platform can automate log generation for some events \(e.g. out of memory FATAL error, javascript ERROR, authentication ERROR, etc.\); in addition, Platform developers can include other logged messages, through ad hoc utility methods \(described in the next section\); each for these can have a specific log level; the “Log level” input field allows to define which logged messages must be saved and others must be ignored: only messages having a log level higher or equal to the ”Log level” are accepted; this is the scale and priorities: FINEST, INFO, DEBUG, ERROR, FATAL; consequently, if “Log level” has been set to “ERROR”, any message having type FINEST, INFO, DEBUG will be ignored, whereas ERROR/FATAL messages are saved. For more details see the section below.

Optional fields that can be specified are:

* **estimated duration **- expressed in seconds, it represents the maximum amount of time Platform will wait for, before generating a DEBUG message for the current elaboration, since it is working for a too long time \(this feature is not supported yet\)

* **notification level** - if specified, an email notification can be automatically sent in case there are messages for the current elaboration, whose log level is higher or equal to the one specified here; for example, if this field is set to ERROR, it means that if there will be messages having ERROR/FATAL log type, an email will be sent

* **max attempts** and **attempt wait time **- these two fields work together and they must be both filled or both set empty. When filled, they allow to automate the restart of an elaboration failed with a FATAL log message \(e.g. out of memory, database connection errors, etc.\). The failed \(FATAL\) elaboration will be re-executed automatically after "attempt wait time" minutes for up to "max attempts" times. If at some point the elaboration completes correctly, it is marked as "completed" whereas all the \(failed\) previous ones \(included the original one\) are marked as "successfully rielaborated with previous errors"

* **tag X / label X **- there are up to 5 tags you can define; a tag represents a piece of data provided to a service in input; for example, in case of a web service \(server-side javascript action\), the request body can contain a complex JSON string, containing a set of attributes; a tag is the attribute name, the label is a more user-friendly description of it. When a couple tag/label has been specified, Platform will automatically extracts the attribute value from the input and save it along with the elaboration; this comes in handy later, when searching for data: instead of searching within the whole body request, the search can search directly for a tag.



