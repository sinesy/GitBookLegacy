## Heap memory analysis

This is a CPU and space consuming feature and should be used carefully.

It will create a temporary dump file in the server file system, related to the current heap memory consumption. After that, the file is automatically analyzed and relevant data fetched. The goad of this feature is helping in identifying an erroneous consumption of memory.

In order to understand the results shown, it is important to know how the heap memory is used and composed of: usually the heap memory contains a wide range of different contents:**entities, data objects, metadata**, etc.

In the end, all of them are composed of basic data, like**strings, numbers, bytes, basic data structures.**Consequently, it must not surprise that the majority of the heap memory is composed of primitive data, which is not very helpful when trying to diagnose an anomalous amount of memory consumption.

For this reason, it is important to pay attention to the objects which are not basic data, but all the others.

[![](http://4wsplatform.org/wp-content/uploads/2018/01/heap-1-1024x988.png)](http://4wsplatform.org/wp-content/uploads/2018/01/heap-1.png)

The result is reported in a dashboard, including the following information:

* **Memory distribution **– it shows how data is spread along the memory: it is likely that the primitive data will be the most representative and the percentage for not primitive data could be so little when compared with raw data that the pie chart could not be able to show it
* **Memory distribution, no basic data **– this is the memory occupation for all data but the raw data; this can be helpful to identify problems related to a too high number of user sessions or metadata instances
* **Occupied space **– another representation of the same content, not expresses in % but in absolute value; in a normal situation metadata should consume a few Mbytes, same for user sessions and server-side javascript objects 
* **Js engines **– in case of multiple executions of server-side javascript actions, as for web services, this is the amount of data instantiated inside the javascript engine: the more web service calls there are, the more javascript engines will be under execution
* **Session Nr **– the number of user sessions currently active, which are related to the number of end users currently using the app; user sessions should never be more the a few hundreds
* **Metadata Nr **– the number of metadata instances, which should be as many as the number of supported languages, per app



