# **Remote Platform servers**

In case of a complex system, composed of series of Platform servers which exchange data with each other, it is helpful to trace togging among all the systems.

Unfortunately, each Platform server would collect logs only for its own monitored services. That means that a “master log repository” is needed, in order to have all logs coming from all systems and search data in it.

Once identified the master repository, it is possible to configure it, in order to retrieve logs collected in remote servers and have these logs locally. This behavior must be carried out behind the scenes, without slowing down the search activity.

In order to setup remote servers in the master repository you have to:

* define in every remote server \(all but the master repository\) an **auth token**: using SqlTool, insert a record in CON58\_ALLOWED\_LINKS; be sure to fill in: APPLICATION\_ID, TOKEN, CREATE\_DATE, USER\_ID\_CREATE, STATUS and ROW\_VERSION; do not set neither EXPIRATION\_DATE nor MAX\_TIMES, otherwise the token would expire sooner or later; this token will be used by the master repository to communicate with this remote server and ask for its local logged data

* in the master repository, open global properties and set parameters **“Remote Platform URL Nr. xxx”** in the MONITOR sub-section, one for each remote server; here you have to define an URL containing the corresponding token just defined for that remote server:

[http://remoteserver:remoteport/platformwebcontext/serviceelaboration/getElaborations?applicationId=....&companyId=...&siteId=...&username=ADMIN&authToken=....&removeSession=true](http://localhost:8280/wag/serviceelaboration/getElaborations?applicationId=ABC&companyId=00000&siteId=100&username=ADMIN&authToken=TOKEN1578562678169&removeSession=true)

  
After doing it, the Platform installation for the master repository will automatically retrieve logged data from remote server every 1 hour. In this way, the amount of data to fetch is limited in size, since the data retrieval is fairly frequent.

Every time data is extracted, it is also removed from the remote repository.

  
You can change the wait time before extraction \(default value: 1hr\) by means of the global parameter **MONITOR -&gt; Wait time before import log \(hrs\)**

  


