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

---

In case a **detail form** is required too, define a “Javascript business component for a form”, where using the method “**getPartialResultOnArchiflow**”, in order to retrieve a list of cards, starting from:

* a document type

* a list of archives

* optional filters

Example:

```js
var json = utils.getDetailOnArchiflow(
  19, // data model id
  reqParams.cardId, // this the unique identifier for the card
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

---

# Designing with Archiflow

In order to store documents in Archiflow, a card is required. A card can contain metadata too, where metadata represents properties associated to the document.

A database table can contain metadata too.

Consequently, the big question is: where is metadata stored? Either in a database table or as card fields.

Let's see both scenarios.



**Metadata stored as card fields**

Pros:

* filtering documents \(cards\) according to its field values
* creation of grids starting from a list of cards, filtered according to document type and/or archive ids
* creation of forms starting from a card 

Cons:

* filtering/ordering conditions are limited, since Archiflow search is not as powerful as it can be a SQL query executed on a set of database tables

Note: if there is a database table where a specific record is linked to a document, it must contains a special field containing the card id; this value represents the document/card identifier



**Metadata stored as table fields in a database**

Pros:

* filtering/sorting documents according not only to table fields but also to fields belonging to other tables grouped through JOIN conditions; 
* a SQL query executed on a set of database tables is powerful and can be used to generate reports, complex grids connecting data coming from different tables

Cons:

* there is a loosing coupling between a record in a table and a document: at least a field in a table must be provided in order to store the document/card identifier, but the purpose of Archiflow would result significantly reduced
* what is the use of Archiflow? must be used by end users not using the Platform web app? If it is so, these users would not be able to access metadata, since there is not any metadata storeed along with the document in a card: it has been stored in the database only!
* how to upload/preview/download documents? only javascript methods could be used for that, since the grid/form is not directly connected to Archiflow: it is connected to a database table! Consequently, the operation of upload/preview/download documents would become more complex to manage \(e.g. where is stored the archive id? the document type? any other data required to store a document?\)

Note: in this second scenario, it is essential to share with the stakeholder the exact usage of cards in Archiflow, in order to avoid losing operations needed on that side, depending on metadata in card not any more stored there.













