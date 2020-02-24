# **Use cases**

**  
How to define monitored services across multiple Platform servers**

Suppose you have multiple Platform applications, connected with each others through web service remote invocations. A specific data flow born on the first server would extend itself to the second one.

The whole data flow would be composed of a set of actions; for example:

* an action \(web service\) to collect data and enqueue it

* an action which process a single piece of information, when dequeued from a queue

* an scheduled action which extracts data just saved and send it to the second server

* on the second server there can be an action \(web service\) which gets data from the remote server and enqueue it

* finally, there is an dequeued action which processes data, bi validating it and saving it on the final destination

In such a complex scenario, it would be a good idea to **define the same service code for each action to monitor belonging to the same data flow**, so that it will be easy to search for elaborations along the same data flow, since each step in the data flow has the same service code and the search can therefore be simply carried out by applying a filter on the service code.

Moreover, if the tagging technique is applied, it would be a good idea to **define the same tag policy along the data flow**: in this way, it would be possible to search for specific piece of data in any part of the data flow and figure out later when there has been a problem.

---

**How to search for errors and their cause**

Starting from the elaborations list, it is possible to filter results by “elaboration state” set ERROR and a time interval.

After locating an error, double click on it to open the elaboration detail window.

Look at the “**Log**” folder to analyze all messages: it is likely to find one reporting the main error. If the error depends on the input data, turn back to the **first folder** to find the data generating the problem, maybe located in the “**request body**” section.

---

**How to trace missing data**

Starting from the elaborations list, **select the right service**: hopefully, remote services connected to the one specified here have been defined using the same service code.

The results list will report all elaborations \(local and remote elaborations\) having the same service code.

If tags have been defined for such service \(in all service definitions, local and remote\), the filter panel will report them as well.

Try to **fill in one or more tags**, so that the results list will be significantly reduced to one transaction only.

After reducing the results, it will be easier to navigate through the elaborations, probably one for each Platform server. Double click on the elaboration having an **ERROR state **and go into depth to its **messages list**: the original error is likely to be located there.

As an alternative, double click on any elaboration matching the filled tags and select the “Logs” folder: press the** “Transaction logs”** button to see all messages for all elaborations of any Platform installation, sharing the same transaction id: not only messages for the current elaboration will be reported, but all of them. Once identified an **error message, double click on it to open the elaboration **which contains it.

---

**How to trace multiple elaborations for the same failed process**

In case an elaboration for a specific service failed with a FATAL log message, it is possible to automate its execution, through the  settings available in the service definition window.

Once done that, the Elaborations window will include all elaborations, including multiple elaborations started from an original failed FATAL elaboration.

In order to filter the elaborations started from an original failed elaboration, just click on the "Show linked elaborations" button: this will limit the elaborations to show to the only ones belonging to the same original failed elaboration.



