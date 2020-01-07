# Subprocess and Call Activiti

In Activiti BPM not only you can create processes, but also sub-processes can be defined. Once a sub-process has been defined, you can link it to any other process, as it were another task of the main process.  
A sub-process can be defined in two alternative ways:

* by defining a sub-process inside the same model
* by defining a process totally independent, i.e. creating a new model and then linking it to another process, by making it a sub-process. In this case, the input parameters required by the sub-process must be passed by the main process.

In the first case, a unique process is created, including its own sub-processes, but these ones cannot be referred \(reused\) in other processes. Each sub-process must have a link to its starting event and another coming out from the ending event.  
In the second case, two distinct processes are created and linked and each of them could be started even separately. Moreover, a special task must be used in order to invoke the sub-process: the Call activity, where all required variables must be passed from the main process to the sub-process and at the end of the sub-process from this one to the parent process.

Properties needed by the Call activity are:

* Id and Name: they identity the task and they are mandatory; be sure NOT to include accents in these fields \(only alphanumeric characters are allowed\).
* Documentation: an optional description of this task
* Called element: id of the sub-process \(mandatory\)
* In parameters \(parameters to pass from the parent process to the sub-process\)
* source: variable id coming from the parent process
* target: variable id defined in the sub-process that would receive the value form the parent variable
* sourceExpression: expression used to fetch a value from the parent process
* Out parameters \(parameters to pass from the sub-process to the parent process, at the end of the execution of the child process\).
* These parameters are similar to the ones specified for the In parameters.

---



