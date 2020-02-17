## How to

## 

First, import an Archiflow Document Type, starting from the Platform **Data Model -&gt; Objects and Relation**: here click on **New** -&gt; **Object from Archiflow**.

Select one or more Document Types to import and press **Next**.

After doing it, Platform will show to the user as list of Archives bounded to each selected Document Type: they come in handy later, when an Archive must be specified to retrieve documents having such document type.



Next, define a “**Javascript business component for a list**”, where using the method “**getPartialResultOnArchiflow**”, in order to retrieve a list of cards, starting from:

* a document type

* a list of archives

* optional filters

  
Example:

```js
var json = utils.getPartialResultOnArchiflow(
  19, // data model id
  [], // filters
  [3, 32767], // int archive ids
  false, // cardsWithAttachedDoc
  null, // int search Types
  null // map additional Settings
);

utils.setReturnValue(json);
```



Finally, a window containing a grid can be filled starting from the “Javascript business component for a list” just defined.

When the grid has been created by Platform, it can be already used but an additional setting is still needed, for working not only with cards, but also with documents linked to cards:

* open the grid definition

* select the Columns folder

* change the column type for CARD\_ID column to “File Id”

* set a default value in insert for the ARCHIVE column: the default value must be the Archive Id where the document will be saved \(and later retrieved\); consequently, the Archive Id to specify must be the same specified in the business component.

Please note that the File Id column should always be declared visible, so that a button will be rendered for it: when clicking such a button, a File Dialog will be prompt to the user, in order to upload, download or preview the document.

  
In case a **detail form** is required too, define a “Javascript business component for a form”, where using the method “**getPartialResultOnArchiflow**”, in order to retrieve a list of cards, starting from:

* a document type

* a list of archives

* optional filters

  


Example:

```js
var json = utils.getDetailOnArchiflow(
  19, // data model id
  reqParams.cardId, // this the unique identifier for the card
  null // map 
  additionalSettings
);

utils.setReturnValue(json);
```



Finally, change the control type for the form:

* open the form definition

* select the Controls folder

* change the column type for CARD\_ID column to “File Id”

* set a default value in insert for the ARCHIVE control: the default value must be the Archive Id where the document will be saved \(and later retrieved\); consequently, the Archive Id to specify must be the same specified in the business component.

Please note that the File Id controls should always be declared visible, so that a button will be rendered for it: when clicking such a button, a File Dialog will be prompt to the user, in order to upload, download or preview the document.

  


