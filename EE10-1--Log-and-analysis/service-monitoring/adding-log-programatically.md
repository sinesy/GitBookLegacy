# **Adding log programmatically to a monitored service**

Apart from the elaborations automatically managed by Platform \(start/end datetime, elaboration state, I/O\), a Platform developer can include additional messages to a specific elaboration, inside a server-side javascript action.

This activity is not essential but can be helpful sometime, to include additional information to read later, when evaluating errors fired by an action.

There are 4 methods available in a javascript action:

**1. method used to add a log message to an elaboration in progress**

This message is not necessarely an error: the developer has to specify its log level too

```js
utils.logServiceElaboration(
  logType,
  logMessage,
  messageCode,
  fileName
)
```

In the simplest case, only the first two arguments must be filled:

* logType: allowed values: FINEST, INFO, DEBUG, ERROR, FATAL

* logMessage

Optionally, it is possible to specify a message code, i.e. a code related to a problem/solution, previously defined \(see the Knowledge Base section\)

In case the current elaboration is about a file to read/write, it is possible to include the file name too. In such a case, it will be created a link between this message and logged files \(see the last section about Searching for logged data\)

---

**2. Method used to set the final elaboration state**

```js
utils.setElaborationState(
  elaborationState,
  result
)
```

In case the server-side javascript action should terminate before the default ending \(with an error\) or simply the outcome must be different from the default one \(all ok\), the Platform developer can specify the outcome. The end datetime is also set automatically by Platform.

Optionally, it is also possible to define the result got back \(if not specified, Platform will automatically gather the result provided by the action through the **utils.setReturnValue\(\)** method\).

Allowed values for elaborationState:

* **S** - started, not finished yet

* **C** - completed correctly

* **E** - interrupted with errors

* **W** - completed with errors; this state should be used programmatically, when there are errors inside a server-side javascript action which are not evaluated as blocking and the service can reach the end; this state is very similar to "C", but it emphasize the presence of errors inside the elaboration

* **R** - re-elaborated, since it was wrong in the pas; this state should never be used programmatically, since it is related to elaboration started automatically by Platform, according to the settings for the monitored service

---

**3. Method to set elaboration state and a message**

This method carries out the same logic described for the previous one, with one more step: append a message to the elaboration; apart from the arguments described above, there are the additional arguments:

* message type; allowed values: FINEST, INFO, DEBUG, ERROR, FATAL

* a message text

* optional message code

```js
utils.terminateElaborationState(
  elaborationState,
  result,
  logType, 
  logMessage,
  messageCode
)
```

---

**4. Method to log a file processing**

This method can be invoked by the Platform developer for the same action/elaboration multiple times: it is used to log the reading/writing of a file. The file names represents the identifier: if the same file name is specified for multiple invocations within the same elaboration, the same record is updated instead of creating a new one.

In this way it is possible to trace the work in progress with the file: under elaboration vs elaboration completed.

```js
utils.logServiceFileElaboration(
  operation,
  elaborated,
  filename,
  dirId,
  backupFileName,
  backupDirId
);
```

The arguments are::

* **operation** - mandatory argument: it represents the kind of elaboration for the file: reading the file or writing it; allowed values;:

* * READ - in case the file has to be read

  * WRITE - in case the file has to be written
* **elaborated** - mandatory: boolean flag indicating whether the operation on the file is still in progress or interrupted with errors \(false\) or the elaboration has been completed \(true\)

* **fileName** - mandatory: the file name in use; in case the file is read/save from the server file system, it should contain the file name only, since the absolute path where saving it is defined through a directory id \(see next argument\); in case the file comes from a remote repository \(e.g. Google Cloud Storage\), the bucket is described through the directory id and the current argument should contain the relative path \(within the bucket\) + the file name

* **dirId**- optional: defines where the file is located

* **backupFileName** - optional: in case the current file has been read and after processing it must be deleted, it could be backed up \(i.e. moved “off-line” to another bucket\); in such a scenario, this is the final name for the backuped file

* **backupDirectoryId** - optional: used in combination with backupFileName; it represents the location of the backuped file

**        
**

