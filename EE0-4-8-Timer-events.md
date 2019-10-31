# Timer events

A timer boundary event can be used to wait for the completion of a manual activity \(user task\).  
Manual activities are a critical part of a process, since they could never be started or completed by the assigned users. In order to unlock the process execution after a specific amount of time, a timer task event can be bounded to an user task: if the task has not been completed in the specified time, the task is stopped and the execution is forwarded towards to the boundary event.

**Note**: there must be always a connection between a timer event and an alternative task to reach after the expiration time, otherwise the process is invalid.

A timer start event works similarly, with the exception that it connects a manual task to listen to the beginning of the task, instead of the completion of it.

This kind of events require the definition of the Id and Name properties, as well as the setting of the following mandatory properties:  
**Time duration** : timer duration.

### Example

**Time date** : starting date/hour of the process/task.  
Allowed format: yyyy:mm:ss \(

### Example

**Time cycle** : repetition of a processo/task.  
Allowed format: R3/PT10H \(repeat 3 times, every 10 hrs\).  
If not specified, the first instance of the processo/task will be started when the process is created, otherwise an alternative date/time can be specified, as well as the cycle time.

---



