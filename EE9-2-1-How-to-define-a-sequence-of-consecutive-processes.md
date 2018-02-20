# How to define a sequence of consecutive processes

Sometimes it can be handful to define a series of processes which are not independent from each other: on the opposite, they must be executed in sequence, one after the other, as in this example:

Process1 -&gt; Process2 -&gt; Process3

In that case, only the first proces must have a scheduling frequency, whereas the other two should be defined as "suspended" and have as "p **arent process** " the previous process.

The two input fields on the bottom of the "Settings" folder have this purpose: they allow to define previous process of the current one, so a sequence is defined; optionally, a " **parent exit code** " can be defined too. Usually a process terminated successfully should return a 0 as exit code, so the parent exit code can be set to 0 if the next process should be invoked ONLY IF the parent process terminates correctly.

This is a complex scenario that can be managed in Platform:

Process 1  
—&gt; terminated successfully with 0 as exit code  
Process 2  
—&gt; terminated with errors with -1 as exit code  
Process 3

In this way, Process 2 would be executed only if Process 1 terminated correctly. y, Process 3 would be executed only if Process 1 terminated with errors.

---



