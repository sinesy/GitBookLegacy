# Client-side integration

The first step is setting up the environment through the application parameters \(Google Domain, admin account, private key, etc.\). A Google Administrator is needed in order to successfully complete this task.

Once completed the initial configuration, the Google SSO can be used on the login page of Platform. Again, application parameters must be defined in order to enable Google SSO.  
See the Identity Management section of Platform user manual to figure out how to define all these settings.

A simple way to embed the Google Calendar or a GDrive folder or GMail is to define a menu item from the "Menu" functionality of the App Designer.  
Select "Create link to web page" to add an embedded web page and choose the "Open on an internal window" check box too.

In case of a  **Google Drive folder** , the URL can be something like that:

[https://drive.google.com/embeddedfolderview?id=XXX](https://drive.google.com/embeddedfolderview?id=XXX)

XXX is the GDrive folder identifier. In order to get it, open Google Drive apart and right click on that folder and copy and paste its id.

Important note: be sure the folder is accessible with the user connected using SSO, otherwise Google will not allow to show its content.

In case of  **Google Calendar** , the URL can be something like that:

[http://www.google.com/calendar/embed?src=:USERNAME](http://www.google.com/calendar/embed?src=:USERNAME)

The URL just reported would filter the calendar events for the current logged user.

In case a common calendar is to be showed, its id must be reported, as for the example below:

[https://www.google.com/calendar/embed?src=XXX@resource.calendar.google.com](https://www.google.com/calendar/embed?src=XXX@resource.calendar.google.com)

the calendar id \(XXX in the example\) can be retrieved by the Google Domain administrator.

---



