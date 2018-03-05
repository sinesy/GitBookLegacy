## Log statistics

This functionality analyzes aggregated data from the application log, in order to **log statistics** about server-side operations, such as CPU/memory consumption, HTTP requests.

[![](http://4wsplatform.org/wp-content/uploads/2018/01/Schermata-2018-01-19-alle-17.52.19-1024x919.png)](http://4wsplatform.org/wp-content/uploads/2018/01/Schermata-2018-01-19-alle-17.52.19.png)

This window is split up in two part: a filter panel on the top and the results area below it.

Through the filter panel you can adjust the time interval on which you want to focus on.

The proposed results are then limited to the aggregated data reckoned in such interval, up to the previous hour.

Aggregated data is automatically calculated every hour, so that the results can be retrieved faster.

The “**force analysis**” check-box can be used to force the reckon of the aggregated data, in case it has never been done in the past \(e.g. the Application Server has been just started up\).

Results are reported in two distinct charts:

* **Total requests nr**, **for each request name**
* **Requests nr **in total + **CPU usage **+ **Memory usage**, along the specified time interval

Optionally, it is possible to click on any request name on the first chart, in order to detail it on the second chart, where the requests nr will be related along the time, only for the selected request name.

This functionality is particularly helpful in case you need to identify which are the most common requests and the peeks for your application over time.

