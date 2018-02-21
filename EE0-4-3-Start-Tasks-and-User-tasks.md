# Start tasks and user tasks

A very common property usually defined in the start task is the name of the user who started the process, in order to refer it in other parts of the process.  
The Start Task includes a property named "initiator" in the Property Inspector, that can be used for that purpose. Be sure to fill in this property with any value but "initiator". That value represents the variable name that you can refer in any other task, through the notation: ${varablename}

On the other side, this initial property just declared must be passed to the process, when starting it.

Another common task is the user task, which represents a manual task started and completed by someone. When choosing this task, some properties must be filled in:

* Id and Name: they identify the task; be sure not to set accents inside the name property
* Documentation: textual description linked to the task \(optional\)
* Assignments: one or more assignees to set for this task \(mandatory\)
* Form properties: additional properties that can be set, according to specific needs.

---



