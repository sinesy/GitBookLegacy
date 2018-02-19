var  **start**  = ** startActivitiProcess** (processId, obj);

* processId: process id

This value can be retrieved from the list of the processes or from the Web Modeler. Example: in the "Execution process list" you can see all the processes. To be more precise, all the versions for all the processes, where a specific process version is expressed as:
SIN&lt;YOUR_COMPANY_ID&gt;_YOUR_COMPANY_ID&gt;_&lt;YOUR_PROCESS_ID&gt;:&lt;VERSION&gt;:&lt;INTERNAL_ID&gt;
The processId to specify must NOT include version and internal id, so it must be something like:
SIN&lt;YOUR_COMPANY_ID&gt;_YOUR_COMPANY_ID&gt;_&lt;YOUR_PROCESS_ID&gt;

* obj: Javascript object containing variables declared in the start event and required in order to start the process.

More precisely, if you have defined variables like MY_EMAIL_ADDRESS and MY_NAME, then the javascript object should contain something like:
{ myEmailAddress: &#8220;&#8230;&#8221;, myName: &#8220;&#8230;&#8221; }
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

startActivitiProcess("PROCESS_ID",obj);
```




                

---


