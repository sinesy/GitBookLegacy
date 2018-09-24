# Google App Engine & Platform

Google App Engine \(GAE\) is a cloud computing platform for developing and hosting web services in Google-managed data centers. Web services can run across multiple servers, with automatic scaling: when the number of requests increases for an application, App Engine automatically allocates more resources to handle the additional demand.

Google App Engine is free up to a certain level of consumed resources. Fees are charged for additional storage, bandwidth, or instance hours required by the application \(web services\).

Google App Engine's integrated Google Cloud Datastore database has a SQL-like syntax called "GQL". GQL does not support the Join statement. Anyway, Datastore is a powerful NoSQL database, able to manage a very high amount of data, in a scalable way, so it represents the perfect choice for some parts of an application, requiring working with big data and do not have the need for analysis of aggregated data, where a relational database or a BI solution can better fit the scenario.



### Platform for GAE

Starting from this brief introduction, Platform can be deployed in a GAE standard environment, in order to scale in seconds, when needed.

Platform suite is composed of different software layers:

* **App Designer** - a web application running on ComputeEngine and using a CloudSQL relational database to manage application configuration
* **Web Interpreter** - a web application running on ComputeEngine and using a CloudSQL relational database or other data sources, representing the configured application running and accessible by the end users; there is one web interpreter instance for each configured application
* **Mobile Interpreter** - a native mobile app, built for Android and iOS platforms, used to run mobile apps, configured starting form the App Designer

When talking about the server-side computation, a weak point is the scalability of a web solution, typically composed of a set of web services. The more requests the web application receives, the more difficult is for the backend to respond with an acceptable timing.

The backend is composed of the web service layer running on Compute Engine \(GCE\) and the relational database, running on CloudSQL, a managed database.

A common production environment is composed of a Google Load Balancer able to forward requests to a number of GCE instances, using the auto-scaling feature provided by Google.

However, this solution can scale in a minute \(the latency time required to startup a new GCE instance\), so not perfect for a peak of requests requiring more a response in seconds.

GAE+Datastore represents a better solution when the auto-scaling needs a response in a second or so.

On the other hand, using a NoSQL database means a lower speed when executing queries and a very simple enquiring language, when compared with the standard SQL.

Starting from these constraints, **Platform for GAE represents a subset of the Web Interpreter** described above, running on GAE and connected to Datastore \(and other Google Cloud Platform services\). You cannot use it to run a web application, but you can create your high-scalable set of web services.

You have still to use a standard Platform installation, running on GCE+CloudSQL and configure a Datastore and objects and business components.

Using the App Designer, you can define web services to run into GAE \(i.e. "Javascript for GAE" actions\).

Once deployed these set of web services on GAE, you can access to them as usual.

Supported features are:

* **metadata export** towards GAE
* **object definition on Datastore**
* **javascript for GAE actions** \(your stateless web services\), including read/write operations on Datastore
* a set of **request alias**, that you can use to call web services
* **authentication** based on a fixed token \(defined once per GAE instance\) or on Platform users
* **Mem-Cache** support, i.e. a cross-instance data cache, where you can store/read values needed across multiple requests or for a long time, in order to avoid costly and slow Datastore queries
* **Task Queue **support, i.e. javascript for GAE actions enqueued into an internal queue, processed one at a time, so that there is a limit to the required computational process and it can also provide a better response to HTTP sync calls. 



### Limitations

GAE cannot be used in a flexible way as for GCE. These are the main limitations:

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

That'all!

Now it is possible to invoke your web services into GAE and enjoy the high-scalability offered by this layer.



### Every-day activities

**Uploading a single action**

Once you have deployed your actions to GAE, you can change any of them multiple times.

You can edit the action definition in the App Designer and send these change to GAE, without exporting the whole application \(Import/Export Application\).

You can send a single action by pressing the "Sync action with GAE" button available on the right fo the window related to the action definition.

Once done that, the changes for your action are already available and up.





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



**Javascript for GAE**

You can define your js actions to run into GAE in a very similar way you already do it when creating server-side js actions: the syntax is the same, i.e. utils.method\(...\)

The difference here is that only a subset of all server-side js methods is available.

You can check out which methods are available by simply pressing CTRL+space inside the js editor when editing a "Javascript for GAE" action.

Basically, the available methods are the ones compatible with GAE, i.e. there are NOT methods involving read/write operations on files or report generations.

Logging operations are supported, as for Server-side Javascript, but it can be accessed only by using GCP console \(see next section for more details\).





**Enqueuing operations into GAE from a GAE web service**

You can use the utils.enqueueAction method from within a "Javascript for GAE" action in order to forward and postpone heavy operations from the main web service to the Task Queue: this design choice is highly recommended, since GAE will interrupt HTTP requests longer than 30 seconds, so in case of complex logic, it would be always a good idea to use queues for managing the real work.





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

