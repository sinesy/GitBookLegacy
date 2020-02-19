# **Introduction**

**    
**This module is able to trace the execution of the following **services**:

* data export from SQL query

* web service remote invocation

* enqueuing and dequeuing of elements from queues

* web services execution and by and large any server-side javascript action

Platform can **automatically trace these events**:

* out of memory

* authentication failure

* javascript syntax errors

* javascript execution errors

* database locks

* data tracking over web service remote invocations

* input/output data \(HTTP request parameters, headers, body, response\)

* execution outcome and errors

* distributed transaction id over remove ws invocations

* internal state

* execution start/end datetime

* current elaboration state \(started, ended, interrupted\)

* tagging some of the input data \(automatically retrieved from the input, up to 10\); these tag values can be used later to search for logged data, filtered by these tags

**Programmatically**, a Platform developer can inject additional events, through server-side javascript utility methods:

* messages to append to the server-side javascript action execution \(a message has a message type having one of the following values: FINEST, DEBUG, INFO, ERROR, FATAL\)

* files to read/write and their state \(in progress, completed\)

* the execution state and outcome

Thanks to these features, it is possible to **define any number of monitored services**, each identified by a service code and automate logging data and behavior. Optionally, a Platform developer can include additional invocations, to fine tune the logging and tracing of the service.

**    
**

![](https://lh6.googleusercontent.com/3rqQn11Wsbac0PUQ0f-56YvBBs4HREiwe3jb-N5rQXQduvUGNG6drL6mluUqT3c-XofhCGY_8hpjFBhvamBmTk0BptgaoPY0xmk9id1NdCL4v6VmXXO1EbqyYesGb9JqcFcfe4sj)

**    
**

Once **configured** a series of services to monitor, Platform will start **gathering data about their execution**, in terms of elaborations, error messages \(and my and large any kind of messages\), processed files \(if there is any\).

Finally, it is possible to **search for elaborations and messages/files**.

Moreover, a **notification** sub-system is available, in order to automate the email notification of some events \(errors\), which can be configured at service level: according to the message type \(e.g. only ERROR or FATAL type messages\), it is possible to notify the event to a specific set of users via email.

**    
**

