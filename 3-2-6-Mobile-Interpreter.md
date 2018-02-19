In addition to the Web Interpreter provided with the Community Edition, a Mobile interpreter is available in the E.E., which consists of

* the Web Designer, used to define Mobile Apps, through the metadata definition
* a server side layer used to synchronize with the app the metadata (the app GUI and behavior), data to and from the central database, the remote database structure mounted on the app
* SQLlite database, used by the app to store/read data and metadata
* a mobile app for Android and iOS platforms, which is able to interpret the metadata defined through the Web Designer and sent to SQLlite and create mobile apps that are deployed through the AppStore or GooglePlay once.

A benefit of this architecture is the maintenance of the app since it can be easily updated any number of times, through the synchronization process supported by 4WS.Platform, which allows the transfer of metadata and data to make the mobile app always up to date.
That task can be accomplished without the need to deploy the app to the AppStore or GooglePlay every time, but just the first time!

                

---


