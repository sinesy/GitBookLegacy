# How to add a FAB button

FAB is an acronym standing for  **Floating Action Button**  and it represents the primary action to perform in a window. It is shown as a button rendered at the bottom right part of the app.  
You can use it to perform a special action, like creating something new, at window level.  
In order to use it, you have to work at window level: open the definition of a window and set the following fields:

* **FAB button action**  – here you have to link a javascript action, executed within the app, which will be invoked when pressing that button
* **FAB button icon**  – an icon to render for the button; for a button used to insert data, it should be selected an icon representing a +
* **FAB button background color**  – used to render something behind the button icon

Bear in mind that the button is rendered at window level, not at panel level, so it would be better not to include the in window more than one panel, otherwise it could confuse the user, since it would not be easy to figure out the purpose/scope of the button.

---



