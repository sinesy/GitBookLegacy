# How to complete a user task from a Javascript action

var  **complete**  =  **completeActivitiTask** \(processInstanceId, obj\);

* processInstanceId: process instance id. This value can be retrieved from the list of process instances or it must be stored in a database table from the inside of a process execution, in order to make it available later.
* obj: Javascript object containing variables declared in the current task.

Note: the  **complete**  variable is a boolean value representing the outcome of the task start and completion.

## Example

var obj = {“outcome”: ‘C’};  
var complete = completeActivitiTask\(args.processInstanceId,obj\);

---



