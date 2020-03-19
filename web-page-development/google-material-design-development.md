# **Google Material Design development**

Google MD is a js library freely available to develop UI based on a theme similar to the one provided by Android mobile platform.

This represents an alternative to the base approach described in the previous chapter. This solution is based on the previous one: you have still to include main\_page.jsp in your own web page: it represents the starting point in order to correctly setup the page content, authenticate on server-side Platform and get the right authorizations.

In addition, you have to include a set of additional js+css files, composing the MD distribution.

It provides:

* a read only grid + store \(both automatically created starting from the panel id\)

* an editable form + store \(both automatically created starting from the panel id\)

* static combobox \(automatically created starting from the selector id\)

* dynamic combobox + store \(both automatically created starting from the selector id\)

* tab folders

* accordion panel

* a panel container based on the “border” layout \(up to 5 embedded regions located at the center, north, south, east and west area of that container\)

* window dialog

* window

**            
**

## **Utility methods directly connected to Platform**

**            
**

### Creating a combo-box store

This is helpful to decode a value in a grid to its translated description.

```js
var store =createComboStore(selectorId);
```

### Creating a grid panel

This method creates both the grid store \(accessible as “store” attribute\) and the grid panel. This grid is always in read only mode.

Supported columns: text, number, checkbox, static/remote combo decoding, date, date+time.ì

```js
var grid = createGrid({
                  panelId: ...,
                  region: ..., // center|north|east/west/south
                  listeners: {
                      rowclick: function(rowIndex,attributeName) {
                        var record = grid.store.list[rowIndex];
                        formPanel.store.baseParams.attrName = record.attrNamexxx;
                        formPanel.load();
                      }
                   }
});
```

### Creating a form panel

This method creates both the form store \(accessible as “store” attribute\) and the form panel.

Supported controls: text number, checkbox, static/remote combo, date, date+time.

```js
var formPanel = createForm({
  title: "....",
  region: ...,
  height: ...,
  labelWidth: ...,
  autoLoadData: false,
  panelId: ...
});
```

**            
**

## **Additional methods**

These methods are connected to Material Design but independent from Platform.

### Creating a window containing panels

```js
var win = new AppWindow({
  title: "...",
  items: [grid,formPanel,...]
});
```

### Creating a dialog

This dialog is automatically shown when instantiated. If the handler callback is not specified, the dialog will be automatically closed. In order to close it programmatically, call d.hide\(\);

```js
var d = new Dialog({
  width: ...,
  height: ...,
  title: ...,
  text: ...,
  buttons: [{
    text: 'Ok',
    handler: function() {
    }
  }
  ]
});
```

### Creating a form store and a form panel

This is an alternative to the createForm method described in the previous section and it allows to programmatically create a form store and, after that, the form panel.

```js
var formStore = new FormStore({
  url: context+"/getdetail?applicationId="+applicationId+"&compId=..."}
);

var formPanel = new FormPanel({
  title: "...",
  region: "...",
  height: ...,
  labelWidth: ...,
  autoLoadData: false,
  store: formStore,
  items: [{
    xtype: 'textfield', // datefield | datetimefield | combo | check
    name: '....', // attr name
    label: '...',
    upper: true,
    width: 350,
    allowBlank: false
  },
  ...
  ]
);
```

Required arguments:

* items - a list of objects, where each object should contain the following attributes:

* * name: "attributename"

  * xtype: "textfield\| filefieldpassword\|numberfield\|datefield\|datetimefield\| button\| combo\| check\|textarea"

  * rows: 1\|2\|...

  * upper: true\|false

  * allowBlank: true\|false

  * disabled: true\|false

  * label: "..."

  * width: xxx

  * allowDecimals: true\|false

  * allowNegativeNumbers: true\|false

  * text: "buttontext"

  * handler: function\(\) {}
* region: "north"\|"center"\|"east"\|"west"\|"south"

Optional arguments:

* store - FormStore linked to this panel, used to fetch data remotely

* title: title to show on the top of the panel

* autoLoadData: true\|false \(default: true\)

* columns: number of label+controls per row

* height - according to the region: mandatory for north/south

* width - according to the region: mandatory for east/west

* listeners - objects containing events:

* * onblur: function\(comp,attributeName,value\)

  * select: function\(comp,attributeName,value\)

Available methods:

* load\(\) - force store loading, which is always asynchronous

* getComponent\(name\) - input control or button, starting from its name

* pull\(alignStore,invalidControlsList\) - get all values from the declared input controls and get back a js object contaning these values, indexed by the control's name. If alignStore is set to true, then update the store.data object too with the same js object

* push\(data\) - set all values to the declared input controls , starting form the js object passed as argument

* clearAll\(\) - clear app all values in the declared input controls

### Creating a grid store and a grid panel

```js
var gridStore = new GridStore({
           url: context+"/getlist?applicationId="+applicationId+"&compId=...."
});

var grid = new GridPanel({
                region: ...,
                store: store,
                colModel: [
                { 
                  dataIndex: "...", 
                  type: "string", // date | datetime | combo
                  header: "...",
                  width: ...
                }
                ,
                …
                ]
);
```

### HTTP requests

Asynchronous request \(best to choose\)

```
newAsyncRequest().send(uri,method,data,mimeType,successCallback [, failureCallback]);
```

Synchronous request

```
var response = newSyncRequest().send(uri[,method[,data]]);
```

### Application Menu

The application menu can be freely created and optionally bounded to the Platform menu definition.

In any case, menu items must be defined with the div named &lt;nav&gt;

Example:

```
<nav class="mdl-navigation">
  <a class="mdl-navigation__link" href="#" 
        onClick="executeFunction('showMyList')" >MyList</a>                
  <a class="mdl-navigation__link" href="#" onClick="logoutFromApp()" >Quit</a>
</nav>
```

You can filter menu items by checking out if specific functionalities are enabled for the current user. You can do it in this way:

```
<nav class="mdl-navigation">
  <% if (is!=null && is.isFunctionIdEnabled("WEBPAGEDEV","articoli")) { %>
  <a class="mdl-navigation__link" href="#" 
        onClick="executeFunction('showMyList')" >MyList
  </a>
  <% } %>            
  <a class="mdl-navigation__link" href="#" onClick="logoutFromApp()" >Quit</a>
</nav>
```

In the previous example, what has been checked out is the abilitation of a functionality whose id is “articoli”. This is the name of a menu item defined in Platform.

If you need to find out which id a functionality has, you have simply to go to the Web Designer UI -&gt; Menu items, then select the functionality you are interested in, press the “Detail” button: in the first folder, Window settings, the functionality id is reported, in the “Title Id” input field.

For a complete example, see Appendix B.

## **Limits**

The Material Design library reported in this chapter has a few limits, reported as follows:

* Grids are read only

* * no currency columns are supported

  * no upload/download columns are supported

Theoretically, it is possible to create an editable grid by adding input controls to single cells and manage programmatically their editability.

In such a scenario, you cannot use the utility methods described in section 2.1, but only the ones described in 2.2 e embedding what missing.

* No tree panels are supported

* Forms

* * no currency fields are supported

  * no upload/download fields are supported

  * no images fields are supported
* No automatic management between grid and form is provided

* No automatic management between a filter panel and a grid is provided

There are many extensions of MD available on the net, which can be included in this version.

A good starting point is

[**https://getmdl.io/components/index.html\#tables-section**](https://getmdl.io/components/index.html#tables-section)

**            
**

