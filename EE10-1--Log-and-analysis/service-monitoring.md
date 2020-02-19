# **Background**

**    
**Example of a distributed system:

![](https://lh3.googleusercontent.com/mD_WFcgcaFebYB737QiDcY6M7fInG0uJC7hTVsUB_BiOF8o4-zJfoAnDecbyWAIwwZKXlzrKSwqXqPS2KEHftlXkYemBNCO-wEPe4cQxl4wn0ITtyOUXbi5YTyVxMO3at-oelacx)

In this scenario, there are 2 distinct applications, each installed in its own Platform server.

Let’s say that the first system is gathering through remote calls a list of sellings from a set of points of sale and it is saving them on its own data repository, through a queue.

Later, these sellings are moved to a second system which has to collect, process and save them.

It would be a good idea to define for both systems the same service code for the “sellings service” \(the same identifier\); in this way, it would be easier to trace data coming from the first system and moved to the second one.

Platform automatically will manage behind the scenes the “distributed transaction”, so that the data born in the first system can be traced with the same transaction id also on the second system.

That will make it easier to search for problems risen along the whole distributed system, since it is possible to filter by datetime interval as well as for service code or transaction id.

In any of the services described in the example above, there is a **wide range of problems **that can happen and interrupt the normal execution flow:

* authentication failed when invoking a remote web service

* too many HTTP requests and consequently request are rejected

* too many database opened connections

* database locks due to incorrect business logic working concurrently on the same set of data

* export too slow or interrupted with errors

* file system reading/writing errors

* syntax errors in server-side javascript actions

* execution errors in server-side javascript actions

* business logic failure in server-side javascript actions, due to invalid input data or data not consistent with the already existing one

* out of memory errors

* too many elements in queue

Moreover, when there is data created on a remote application and sent to another one, i.e. when there is a **distributed system**, something can go wrong in any of the involved components and it is important to track the same data along the whole system, which represents additional problems to take into account.

**    
**

