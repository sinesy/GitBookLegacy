## Cleaning up data

In order to speed up the synchronization process, both for metadata and data, Platform prepares the metadata database and the data to send to each mobile device in advance: in this way, the sync process is reduced in terms of wait time, since data has been already prepared.

The drawback of this solution is that it consumes space in the server. Space is consumed for:

* preparing metadata database for each device of each user
* preparing data \(read/write and read only data\) each device of each user

In case of a development environment, this effect is even worse, since it is likely to use simulators for devices or in any case to uninstall and re-install the app multiple times. That means many devices are created \(and never removed\) for the same user. As a consequence, Platform prepares a lot of data for devices which will never be used any more.

Moreover, there could be \(real\) users who never and very rarely would synchronize, but metadata and data is prepared for them as well, as for any other device.

For reducing the amount of space required for these operations, Platform provides 2 important settings, which have the purpose of deleting useless data from the server file system:

* an application parameter \(**MOBILE -&gt; Days nr before deleting devices**\) defining the maximum number of days after that a device will be deleted from the system, if it has not synchronized at least once in that time. Thanks to this parameter, sync process is faster, since data will not be duplicated for each device of the same user and consequently also the required space on the file system is reduced

* "**Data delete wait time**" setting \(expressed in days\), available in the **application detail **\(mobile section\), used to delete from the file system all files older than the specified number of days; this parameter will remove old data for devices who never synchronize, independently of the value of the previous parameter. In case a device will synchronize after a long time and data for it has been already removed, the whole data will be recreated and only for it, the sync process would be longer than usual.



