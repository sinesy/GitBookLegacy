# Gateways

**Parallel gateway** : this special kind of gateway does not evaluate any condition during its execution. Its purpose is to allow the concurrent execution of tasks, belonging to different paths of the process. All parallel paths coming into this gateway are blocked and the execution is suspended until all the coming flows have been completed. At this point, the out link is enabled and the execution is restared.  
 **Exclusive gateway** : this is a very common task; this gateway evaluates conditions applied to each out arch and allows the execution of the only sequence flows whose conditions are valid.

### Example

${TEXT\_VALUE == ‘true’}  
${NUMERIC\_VALUE == 123}

---



