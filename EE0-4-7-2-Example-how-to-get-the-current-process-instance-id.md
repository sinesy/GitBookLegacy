# Example : how to get the current process instance id

A process instance id identifies a specific process execution. This data can be useful in case an external application needs to refer a specific process executiion.

```js
try {
  var processInstanceId = execution.getVariable("processInstanceId");
  execution.setVariable("PROCESS_INSTANCE_ID", execution.getProcessInstanceId());
} catch(e) {}
```

**Note**   
In order to create a link between a record in an application and a specific process execution, two alternative approaches are feasible:  
the external application starts a process and stores the process instance id inside a record into an application managed table; no record ids are supposed to be passed to the process execution  
the invoked process would receive in input a record id and it can use it to store in the record its process instance id.

---



