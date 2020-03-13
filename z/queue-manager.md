# Queue Manager

In a complex Enterprise Application there could be many processes under execution on the server-side, each one could consume a significant amount of CPU and memory and could last a while.

Moreover, sometimes it could be dangerous to execute simultaneously processes working on the same set of data, because they could create locks which blocks the execution of these processes and even lead to a dead lock.

A typical solution to all these issues is the same: **queues**.

A queue is a special persistent storage where a sequence of processes to execute are enqueued and performed one at a time, starting from the first insert till the last one \(FIFO policy…\)



Platform allows you to define **any number of queues.**

When you want to include a process in a queue, you have simply to specify the **queue name** and, optionally, a **priority**.

The priority is a number you can use to move a process before another. If you use it, you are not any more using a FIFO queue, but a priority based queue.

Optionally, you can also define a **waiting time**: a time, expressed in milliseconds that the process has to way before being executed.

Processes managed by queues can be: 

* **server-side javascript actions**
* **web services to invoke**
* **shell commands to execute**

According to the process type, Platform provides 3 different methods.The only way to work with queues is to define server-side javascript actions.

These are the signatures for these 3 methods:

**1. Enqueuing server-side js actions**

```
var ok = utils.enqueueAction(queueName, actionId, params, priority, processWaitTime, logExecution);
```

The arguments are:

* **queueName** – optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue

* **actionId** – server-side javascript action identifier to execute

* **param** – javascript object containing parameters to pass to the action

* **priority** – optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueuing time

* **processWaitTime** – optional; if specified, the process will not be started before that time, expressed in seconds

* **logExecution** – true to log in the predefined table LOG60\_LOGS the execution of the process

Note: the javascript object specified through the "param" can accept an optional attribute named "**queueTimeout**": when the action execution time overpasses that value, \(expressed in minutes\), the element is marked as "timeout" in the queue and the queue is then unlocked, in order to allow extracting new elements from it. Note that the current action is still under execution and this could create drawbacks in case of actions which should be executed sequentially, since the work on the same set of data,by writing them.  


**2. Adding a web service invocation as a process to a specific queue.**

```
var queueId = utils.enqueueWebService(queueName, url, params, priority, processWaitTime, logExecution);
```

The required arguments are:

* **queueName** – optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue

* **url** – shell command to execute

* **param** – js object containing parameters to pass to the web service

* **priority** – optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueing time

* **processWaitTime** – optional; if specified, the process will not be started before that time, expressed in seconds

* **logExecution** – true to log in LOG60\_LOGS the execution of the process  

**3. Adding a shell command as a process to a specific queue.**

```
var queueId = utils.enqueueShellCommand(queueName, cmd, priority, processWaitTime, logExecution);
```

The required arguments are:

* **queueName** – optional: queue name; if not specified, the process will be enqueued in the DEFAULT queue

* **cmd** – shell command to execute

* **priority** – optional; if specified, processes within the same queue will be sorted according to the priority rathe than to the enqueing time

* **processWaitTime** – optional; if specified, the process will not be started before that time, expressed in seconds

* **logExecution** – true to log in LOG60\_LOGS the execution of the process

  


It is likely to use one queue only: **using multiple queues can be risky in case of parallelizing process executions**, since they could create locks if working on the same set of tables, so you have to carefully think about the need for multiple queues!

The App Designer also provides an administration console where all enqued processes are reported, as well as the processes under execution.

As soon as a process under execution terminates, it is removed from that console and the queue, and there will not be any trace about it.

You can access to that console through: **Administration -&gt; Process Queues**

Here you can find the list of all processes, their **process name, type, priority, current status**.

This console also provides buttons to **force the termination of a process**: when pressing that button, the process is removed from the queue, but it is still running. There is no way to terminate it.  


The “Force Start” button is used to **force the execution** of the selected process in the list: independently of the position of that process in the queue, it will start immediately.

Pay attention to this operation: locks could be created in the database if the process forced to start is working on the same set of data the other processes are using.

It is also possible to force termination and starting of waiting processes also from javascript.



  


