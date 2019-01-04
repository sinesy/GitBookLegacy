# Google App Engine & Platform

Google App Engine \(GAE\) is a cloud computing platform for developing and hosting web services in Google-managed data centers. Web services can run across multiple servers, with automatic scaling: when the number of requests increases for an application, App Engine automatically allocates more resources to handle the additional demand.

Google App Engine is free up to a certain level of consumed resources. Fees are charged for additional storage, bandwidth, or instance hours required by the application \(web services\).

Google App Engine's integrated Google Cloud Datastore database has a SQL-like syntax called "GQL". GQL does not support the Join statement. Anyway, Datastore is a powerful NoSQL database, able to manage a very high amount of data, in a scalable way, so it represents the perfect choice for some parts of an application, requiring working with big data and do not have the need for analysis of aggregated data, where a relational database or a BI solution can better fit the scenario.

### Platform for GAE

Starting from this brief introduction, Platform can be deployed in a GAE standard environment, in order to scale in seconds, when needed.

The Platform suite is composed of different software layers:

* **App Designer** - a web application running on ComputeEngine and using a CloudSQL relational database to manage application configuration
* **Web Interpreter** - a web application running on ComputeEngine and using a CloudSQL relational database or other data sources, representing the configured application running and accessible by the end users; there is one web interpreter instance for each configured application
* **Mobile Interpreter** - a native mobile app, built for Android and iOS platforms, used to run mobile apps, configured starting form the App Designer

![](/assets/gae_no.png)

When talking about the server-side computation, a weak point is the scalability of a web solution, typically composed of a set of web services. The more requests the web application receives, the more difficult is for the backend to respond with an acceptable timing.

The backend is composed of the web service layer running on Compute Engine \(GCE\) and the relational database, running on CloudSQL, a managed database.

A common production environment is composed of a **Google Load Balancer able to forward requests to a number of GCE instances**, using the auto-scaling feature provided by Google.

However, **this solution can scale in a minute** \(the latency time required to startup a new GCE instance\), not so perfect for a peak of requests requiring a more responsive solution.

GAE+Datastore represents a better solution when the auto-scaling **needs the creation of new instances in a second** or so.

On the other hand, using a NoSQL database means a lower speed when executing queries and a very simple enquiring language, when compared with the standard SQL.

Starting from these constraints, **Platform for GAE represents a subset of the Web Interpreter** described above, running on GAE and connected to Datastore \(and other Google Cloud Platform services\). You cannot use it to run a web application, but you can create your high-scalable set of web services.

You have still to use a standard Platform installation, running on GCE+CloudSQL and configure a Datastore and objects and business components.

Using the App Designer, you can define web services to run into GAE \(i.e. "Javascript for GAE" actions\).

Once deployed these set of web services on GAE, you can access to them as usual.

![](/assets/gae_arc.png)

Supported features are:

* **metadata export** towards GAE
* **object definition on Datastore**
* **javascript for GAE actions** \(your stateless web services\), including read/write operations on Datastore
* a set of **request alias**, that you can use to call web services
* **authentication** based on a fixed token \(defined once per GAE instance\) or on Platform users
* **Mem-Cache** support, i.e. a cross-instance data cache, where you can store/read values needed across multiple requests or for a long time, in order to avoid costly and slow Datastore queries
* **Task Queue **support, i.e. javascript for GAE actions enqueued into an internal queue, processed one at a time, so that there is a limit to the required computational process and it can also provide a better response to HTTP sync calls. 

### Limitations

GAE + Platform cannot be used in a flexible way as for GCE. These are the main limitations:

* only **stateless web services** are supported. It means you have to design your javascript for GAE actions so that they can work without internal state linked to a user, but everything needed must be passed forward
* **up to 10 queues** can be defined
* a single queue execution **cannot run for more than 10 minutes**
* **no access to file system** is allowed, so reading/writing files should not be carried out using GAE

### Setup

In order to use Platform for GAE, a few steps must be followed:

* **create a GAE instance** in an already existing Google Cloud Project, the same where GCE and CloudSQL have been configured and where a standard installation of Platform is available; here it is essential to **pay attention to the region when the GAE will be installed**: it cannot be changed later, so it is important to set it correctly
* **deploy Platform for GAE** into the just configured GAE instance
* through the App Designer, some **Global parameters must be defined**, in the GOOGLE folder, in order to correctly setup the connection with the right Google Cloud project and Datastore:
  * Google Service Account Email
  * Google Service Account Key
  * Google Datastore Id
* through the App Designer, the Application parameter named **"Password Platform for GAE" must be defined**, in the GOOGLE folder, in order to correctly setup the connection with the Google App Engine, used to communicate with it and send application metadata or other operations

At this point, it is possible to start creating objects for the Datastore and define Javascript for GAE actions, which will be later executed inside a GAE instance.

Optionally, it is possible to define request alias for the actions just created.

Once the configuration process for your application has been completed, you can export metadata to GAE:

* select Application -&gt; Import/Export Application
* go to "Metadata Application Management" folder
* press the Export metadata to Platform for GAE

That's all!

Now it is possible to invoke your web services into GAE and enjoy the high-scalability offered by this layer.

### Every-day activities

**Uploading a single action**

Once you have deployed your actions to GAE, you can change any of them multiple times.

You can edit the action definition in the App Designer and send these change to GAE, without exporting the whole application \(Import/Export Application\).

You can send a single action by pressing the "Sync action with GAE" button available on the right fo the window related to the action definition.

Once done that, the changes for your action are already available and up.

---

**Enqueuing operations into GAE from your web application**

A very common integration scenario between your web application running on GCE and web services available in GAE is related to the execution of computations within GAE, using the Task Queue feature, i.e. by enqueuing these operations into GAE, instead of running them in the standard Platfom queues.

Forwarding these operations outside of a standard Platform environment has the big advantage of reducing the computation effort required by GCE and use GAE for whay it is designed for: high scalability with multiple requests.

For this reason, you can use a new js method available in a server-side js action:

```js
var uuid = utils.enqueueGaeAction(String queueName,Long actionId,Map params)
```

This method will forward the execution of the action identified by actionId to GAE, so actionId myst be a "Javascript for GAE" action; in GAE the execution will be enqueued in the queue identified by "queueName".

The method will get back a UUID value representing the unique identifier for the enqueued element, in case it would be helpful to trace it in your web application.

A few limitations:

* up to 10 queues are available in GAE; this value could be changed when deploying Platform for GAE, but it is not recommended, since it could be pretty expensive to increase it, in terms of billing
* up to 5 tasks per seconds are allowed to be executed in a single queue in GAE
* no postponed actions can be enqueued \(as for server-side javascript enqueueAction method\)
* queue execution is not reported inside the App Designer: it can be monitored only by using the GCP console, in the section App Engine -&gt; Task Queues

---

**Javascript for GAE**

You can define your js actions to run into GAE in a very similar way you already do it when creating server-side js actions: the syntax is the same, i.e. utils.method\(...\)

The difference here is that only a subset of all server-side js methods is available.

You can check out which methods are available by simply pressing CTRL+space inside the js editor when editing a "Javascript for GAE" action.

Basically, the available methods are the ones compatible with GAE, i.e. there are NOT methods involving read/write operations on files or report generations.

Logging operations are supported, as for Server-side Javascript, but it can be accessed only by using GCP console \(see next section for more details\).

---

**Enqueuing operations into GAE from a GAE web service**

You can use the utils.enqueueAction method from within a "Javascript for GAE" action in order to forward and postpone heavy operations from the main web service to the Task Queue: this design choice is highly recommended, since GAE will interrupt HTTP requests longer than 60 seconds, so in case of complex logic, it would be always a good idea to use queues for managing the real work.

For an example, see the section below.

---

**Executing public web services on GAE**

It is strongly recommended to design web services in GAE \(i.e. actions having type "javascript for GAE"\) so that they are asynchronous, that is to say, they should always be coupled to a second "javascript for GAE" action to enqueue the elaboration internally, so that the real elaboration is executed in the queue and the web service can terminate immediately.

Bear in mind that a single HTTP request never can last for a long time: App Engine interrupt with error an HTTP request every time it lasts more than 60 seconds. 

You can do it, by following these steps:

1.create your internal action "javascript for GAE" which will elaborate your request; let's say that it has xxx id

2.create your public web service, i.e. another action "javascript for GAE" which will be invoked by any external client and \(i\) enqueue the input data to the first action and \(ii\) will provide a response to the client; let's say that it has yyy id

```js
var uuid = utils.enqueueAction(
      "MY_QUEUE_NAME", // queueName
      xxx, // actionId
      vo, // // my input data, expressed in JSON format
      null, // priority is ignored
      null, // processWaitTime is ignored
      false // logExecution is ignored
);
utils.setReturnValue(JSON.stringify({ success: true, uuid: uuid }));
// in this way, you can trace your enqueued action, starting from the uuid, if needed
```

3.define a request alias for  your public web service,  where you have to internally provide the appId, the action id and either the token or the standard credentials appId+companyId+siteId+username.

```js
/executeJs?actionId=yyy&appId=MYAPPID&token=MYAUTHTOKEN
```

```
/executeJs?actionId=yyy&appId=MYAPPID&companyId=...&siteId=...&username=...&password=...
```

It is strongly recommended to pass sensitive information in the request header rather than as request parameters, in this way they will be encrypted by HTTPS when executing the request.

Your auth  token is set as default value like the Google Project Name; in any case, it is the same specified as "GAE Password" value for the app parameter in the App Designer.

As an alternative, you can specify user credentials:

```js
/executeJs?actionId=yyy&appId=MYAPPID&companyId=...&siteId=...&username=...&password=...
```

1. You are now ready to invoke your public web service:

```
https://yourgoogleprojectname.appspot.com/alias?cmd=MY_ALIAS&appId=...
```

You can use both GET and POST HTTP methods.

---

**Executing queries on Datastore**

Platform for GAE was born to provide high scalability. This goal can be reached only if a few constraints are fulfilled:

* use only stateless web services
* use the MemCache as much as possible, to minimize the access to a database
* connect only to a high scalable database, that is to say, the NoSQL Google Datastore

If you need to read or write instructions on Google Datastore, you can use the same javascript instructions available in the standard installation of Platform, described below.

First, you have to declare your objects, one of each "entity" \(e.g. table...\) you want to manage in Datastore:

* select the "Data Model" menu and choose "Objects and relationships"
* press the Add button and then "Add Object to Datastore"
* Here you have to assign a name to the object, in camel-case and with the first letter in uppercase \(e.g. OrderRows\)
* Add as many fields as you need and choose a field as primary key; it is strongly recommended to choose a string type \(or directly an UUID type\)  field for the primary key and assign to it an UUID value, which does not require additional queries to be reckoned. That means you should always avoid to choose a counter for the primary key: it is not the faster choice

Once you have created your objects, you can start using them in actions having type "Javascript for GAE" and create your web services to read or write data in the corresponding entities.

**Reading data \(using GQL - Google query language for Datastore\)**

```js
var json = utils.executeQueryOnGoogleDatastore("select * from Intro",9,true,[]);
//utils.log(json,"DEBUG");
utils.setReturnValue(json);
```

**Important note:** DO NOT use the previous method to execute a query whose purpose is reading a single record, starting from the primary key: the "executeQueryOnGoogleDatastore" operation is "expensive" and should not be used when it is not needed, i.e. when you need to read a single record by primary key.

Bear in mind that all reading/writing operations \(except for reading an entity by primary key\) are pay-per-use operations: the more you call them, the more you pay.

In case of reading an entity  by primary key use the next method

**Reading a single entity by primary key:**

```js
var vo = getEntity(
  entityName, // name of the entity, in camel-case (e.g. "OrderHeaders")
  key, // the primary key, typically a String type
  maxCachedEntities // max number of entities read from this method which will be stored in cached, 
  // instead of being retrieved from datastore; the cache can be cleared up, by using "clearDatastoreEntities" method
); // vo is a javascript object, the entity
```

**Insert data:**

```js
var outcome = utils.insertObjectOnGoogleDatastore
  vo, // the js object to insert, having attributes compatible with the ones defined in the entity
  xxx, // dataModelId corresponding to the entity where writing data
  true // interruptExecution
);
```

**Update data:**

```js
var outcome = utils.updateObjectOnGoogleDatastore(
  vo, // the js object to insert, having attributes compatible with the ones defined in the entity
  xxx, // dataModelId corresponding to the entity where writing data
  true // interruptExecution
);
```

**Delete data:**

```js
var outcome = utils.deleteObjectOnGoogleDatastore(
  vo, // the js object to insert, having attributes compatible with the ones defined in the entity
  xxx, // dataModelId corresponding to the entity where writing data
  true // interruptExecution
);
```

---

**Executing queries on CloudSQL**

Platform for GAE was born to provide high scalability. This goal can be reached only if a few constraints are fulfilled:

* use only stateless web services
* use the MemCache as much as possible, to minimize the access to a database
* connect only to a high scalable database, that is to say, the NoSQL Google Datastore

Consequently, you should avoid reading or writing data to external systems, including a relational database.

Optionally, you could connect App Engine to CloudSQL, the managed relational database provided by Google, having a MySQL implementation.

Consequently, you have the chance to directly access this database instance, if correctly set up in the Google Console for the same Google Cloud Project.

Since the CloudSQL instance cannot provide the same scalability of Datastore, it should be used carefully.

Please have a look at this section to get more details about that:

[https://cloud.google.com/sql/docs/mysql/connect-app-engine](https://cloud.google.com/sql/docs/mysql/connect-app-engine)

If you decide to directly connect App Engine to a CloudSQL, please respect the following steps:

* try to use the MemCache as much as possible, instead of reading data from CloudSQL
* check if data you need from CloudSQL is already available in cache, only in case it is not, then read it through a query

This hint can ensure as much scalability as you need, if queries are always the same.

Once you have created  your objects linked to CloudSQL, you can start using them in actions having type "Javascript for GAE" and create your web  services to read data in the corresponding tables.

**Reading data**

```js
var list = []; // please do not do it for long result sets!
var readRow = function(vo) {
    //utils.log(JSON.stringify(vo),"DEBUG");
    list.push(vo);
}

utils.executeQueryWithCallback("readRow","SELECT * FROM PRM01_USERS",null,false,true,[]);
utils.setReturnValue(JSON.stringify(list));
```

As you can see from the example above, you can only read a single row at a time, in order to reduce the amount of memory needed to read a long result set; you should avoid accumulating records as in the example, but simply process each record when available in the callback function.

**Writing data**

```js
var numberOfProcessedRecords = utils.executeSqlNoLog(
  sql,
  null,  // dataStore id
  false, // separatedTransaction
  true,  // interruptExecution
  []     // parameters
);
```

---

**Logging on GAE**

As for Server-side Javascript, you can still use the utils.log\(...\) method to log messages within your actions runed into GAE.

Please pay attention to the number of log operations you include in your actions: if they have beed included for debugging purpose, they should also be removed at some point.

It is highly recommended to remove useless logging operations, since they could increase the total billing for your web services running on GAE.

In order to see the logged messages, you have to access the GCP console and

* go to StackDriver -&gt; Logging
* choose the right GCP project and select "GAE Application, Default server"

Messages will be shown automatically, according to these selections and other optional filters, from the least recent to the most recent \(on the bottom\).

![](/assets/gae.png)

Each line reports a single HTTP request, request time, outcome, etc.

When expanding a single line, related to a specific HTTP request, you can see all logged messages related to that request.

![](/assets/gaede.png)

