Global variables can be included in SQL instructions and/or on the sync rules. They are automatically replaced by the run time value of that variable.
This is the list of currently supported variables:

:APPLICATION_ID &#8211; application identifier
:BASE_URL &#8211; server base url
:COMPANY_ID &#8211; company identifier (used in case the app supports partitioned data)
:SITE_ID &#8211; site identifier
:USERNAME &#8211; current user
:UUID or :DEVICE_ID &#8211; device id, i.e. a unique identifier for a specific device (more specific than the username)
:LANGUAGE_ID &#8211; current user
:DOCUMENTS_DIR &#8211; absolute path within the mobile device, where files are stored;it is a folder inside the "customFiles" default app folder.
:TODAY &#8211; current date
:NOW &#8211; current date+time
:YEAR &#8211; current year
:GPS_LATITUDE &#8211; current latitude
:GPS_LONGITUDE &#8211; current longitude
:GPS_ALTITUDE &#8211; current altitude
:GPS_SPEED &#8211; current speed
:APP_VERSION &#8211; current app versione
:LAST_SYNC_DATE &#8211; last sync date



                

---


