# Google Calendar

With this integration developers can automate the creation and management of calendar events in the user’s main calendar. This feature is not intended for Google Calendar UI substitution, but for basic and automatic operations: creation, update and deletion of an event.  
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE\_SERVACC\_EMAIL
* GOOGLE\_SERVACC\_KEY

to enable the Google Apps integration and the 4WS.Platform user must be a Google Apps user.  
The Javascript actions available are the following.

## Add a calendar event in the main calendar of a Google Apps for Work Account

#### Syntax

```js
utils.addGoogleCalendarEvent(title, beginDate, endDate)
```

#### Details

**title**  – the title of the event  
 **beginDate**  – the beginning date and time of the event  
 **endDate**  – the ending date time of the event

#### Example

this example shows how to call the method from a Javascript Server action and get the id of the event. The full list of fields can be found in the Java org.wag.valueobjects.java.CalendarEvent class.

```js
var cal = utils.addGoogleCalendarEvent('My new event', new Date(2014,8,26,11,00), new Date(2014,8,26,12,00));
utils.setReturnValue('{ "id":"' + cal.id +'" }');
```

After this we can for example use a JDBC call to save the id in a DB.  
If the return value of the server call is needed on the client side, a Javascript client call can be set up to get the JSON object representing, in this case, the id \(the actionId is the id of the Javascript Server action\):

```js
var response = new SyncRequest().send(
    contextPath+"/executeJs?applicationId=&lt;appId&gt;" +
    "&amp;actionId=&lt;actionId&gt;",
    "POST",
    null
);
alert(response);
```

## Modify a calendar event

#### Syntax

```js
utils.modifyGoogleCalendarEvent(calendarEventId, title, beginDate, endDate)
```

#### Details

**calendarEventId**  – the id of the event  
 **title**  – the title of the event  
 **beginDate**  – the beginning date and time of the event  
 **endDate**  – the ending date time of the event

#### Example

modify the title of an event

```js
utils.modifyGoogleCalendarEvent('','Modyfied title',null,null);
```

## Delete a Google Apps calendar event

#### Syntax

```js
utils.deleteGoogleCalendarEvent(calendarEventId)
```

#### Details

**calendarEventId**  – the id of the event

---



