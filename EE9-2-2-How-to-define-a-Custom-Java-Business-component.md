# How to define Custom Java Business component

A Java programmer can create a java class to invoke through the scheduler. This class must implement a specific Java interface described below. Once compliled that class, it must be deployed into Platform and the Platform service must be restarted, otherwise the class cannot be accessed by the Java classloader of the Application Server.

They must implement a specific interface provided by Platform:  **it.sinesy.wag. scheduler. java.ScheduledProcess** . That class forces the programmer to implement the following method:

**public ScheduledProcessMessage startSchedProcess\(UserInfo userInfo, Con48SchedProcess processVO,Object\[\] params\) throws Throwable { … }**

The returning object would contain the outcome of the process execution and an optional message \(e.g. the error message\). Usually a "0" outcome value means a process completed correctly.

The method arguments have the following meaning:  
 **UserInfo**  – it contains the settings \(e.g. the language code to use\) linked to the user specified when defining the sheduled process; it is optional. It can be helpful in case a process needs a specific language to work with.  
 **Con48SchedProcess**  – the process settings \(e.g. the process name, etc.\)  
 **Object\[\]  ** – optional parameters, defined when creating the process.

---



