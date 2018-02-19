Grid or detail form panels automatically render a toolbar above them.
According to the number of commands in such a toolbar, if there is not enough space for all of them, a popup menu is rendered on the top right part of the app, instead of the toolbar.
The  **default buttons ** are:

* insert &#8211; used to create data in a form
* delete &#8211; used to delete one or more rows in a grid o the current data in a detail form
* save &#8211; used to save current edited data in a detail form

The visibility of these buttons is driven through the corresponding definition windows: just (un)select the check-boxes available at grid/form level to hide/show these buttons.

Moreover, you have the chance to add further buttons, through the &#8220; **Custom buttons** &#8221; subfolder. These buttons are shown after the default buttons described above.
Again, you can hide them through the same feature.

In case you need to enable/disable custom buttons dynamically, when a specific event happens, you can use a javascript action listening to such event and exploit the following built-in methods:

```js
setEnabledPanelButtonXXX(buttonId, enable);
```

These method works on the panel identified by the XXX id, where

* &#8220;buttonId&#8221; represents the button identifier that you can find in the buttons list (Id column)
* &#8220;enable&#8221; is a boolean value, used to enable/disable the button.


                

---


