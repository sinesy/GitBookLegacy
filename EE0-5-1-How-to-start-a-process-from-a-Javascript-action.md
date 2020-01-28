# How to start a process from a JavaScript action

var  processInstanceId  = ** startActivitiProcess** \(processId, obj\);

* processId: process id

This value can be retrieved from the list of the processes or from the Web Modeler. Example: in the "Execution process list" you can see all the processes. To be more precise, all the versions for all the processes, where a specific process version is expressed as:  
SIN&lt;YOUR_COMPANY\_ID&gt;\_YOUR\_COMPANY\_ID&gt;_&lt;YOUR_PROCESS\_ID&gt;:&lt;VERSION&gt;:&lt;INTERNAL\_ID&gt;  
The processId to specify must NOT include version and internal id, so it must be something like:  
SIN&lt;YOUR\_COMPANY\_ID&gt;\_YOUR\_COMPANY\_ID&gt;_&lt;YOUR\_PROCESS\_ID&gt;

* obj: Javascript object containing variables declared in the start event and required in order to start the process.

More precisely, if you have defined variables like MY\_EMAIL\_ADDRESS and MY\_NAME, then the javascript object should contain something like:  
{ myEmailAddress: “…”, myName: “…” }  
that is to say, variable names must be expressed in "camel-case".

Note: the  **start**  variable is a boolean value representing the outcome of the process start.

## Example

```js
var obj = {
  requestDate: new Date(),
  docId: vo.documentId,
  requestId: vo.requestId,
  initiator: vo.requestUserId
};

var processInstanceId = null;
try {
  processInstanceId = startActivitiProcess("PROCESS_ID",obj);
}
catch(e) {
  // in case of failure when attempting to start a process, an exception is fired here: e.toString() contains the error message
}
```

---



