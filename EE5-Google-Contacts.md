# Google Contacts

With the Google contacts integration, developers can read the user contact list and retrieve data to use, for example, in Javascript actions.  
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE\_SERVACC\_EMAIL
* GOOGLE\_SERVACC\_KEY

to enable the Google Apps integration and the 4WS.Platform user must be a Google Apps user.  
The Javascript actions available are the following.

## Get a list of contacts/emails from the user’s Google Apps contact list

#### Syntax

```js
utils.getGoogleContactsFiltered(pages, maxPageResults, searchString, splitEmails)
```

#### Details

**pages**  – \(can be null\) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.  
 **maxPageResults**  – \(can be null\) the max number of contacts to retrieve in every call. If null the Google default limit is used.  
 **searchString**  – \(can be null\) a search string used for full text search on contacts.  
 **splitEmails – ** \(can be null\) boolean value that indicates to create more contacts results in case of multiple e-mail addresses for a single contact.

#### Example

Fetch all emails in the contacts list

```js
utils.getGoogleContactsFiltered(null,null,null,null);
```

Be careful because this example may use a lot of Google API calls depending on the number of contacts. To limit the calls and data exchanged use something like:

```js
utils.getGoogleEmailContactsFiltered(3,150,’John’,false);
```

IMPORTANT NOTES:  
The number of email addresses retrieved can be different from the number of contacts, if contacts have 0 or more than 1 email addresses, in case of splitted emails.

## Get a list of contacts/emails from the Google Apps domain shared contact list

#### Syntax

```js
utils.getGoogleSharedContactsFiltered(pages, maxPageResults, searchString, splitEmails)
```

#### Details

**pages**  – \(can be null\) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.  
 **maxPageResults**  – \(can be null\) the max number of contacts to retrieve in every call. If null the Google default limit is used.  
 **searchString**  – \(can be null\) a search string used for full text search on shared contacts.  
 **splitEmails – ** \(can be null\) boolean value that indicates to create more contacts results in case of multiple e-mail addresses for a single contact, .

#### Example

fetch all contacts in the contacts list

```js
utils.getGoogleSharedContactsFiltered(null,null,null,null);
```

Be careful because this example may use a lot of Google API calls depending on the number of contacts. To limit the calls and data exchanged use something like:

```js
utils.getGoogleContactsFiltered(3,150,’John’,false);
```

IMPORTANT NOTES:  
The contact may not contain an email address.

## Add a contact to the user’s contact list or to the domain shared contact list

#### Syntax

```js
utils.addGoogleContact(name, surname, email, phone, shared)
```

#### Details

**name**  – the name of the contact.  
 **surname**  – the surname of the contact.  
 **email**  – the e-mail of the contact.  
 **phone**  – the phone of the contact.  
 **shared**  – \(can be null\) true if the contact must be stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.

## Updates the contact of the user’s contact list or the domain shared contact list

#### Syntax

```js
utils.updateGoogleContact(contactId, name, surname, email, phone, shared)
```

#### Details

**contactId**  – the id of the contact.  
 **name**  – the name of the contact.  
 **surname**  – the surname of the contact.  
 **email**  – the e-mail of the contact.  
 **phone**  – the phone of the contact.  
 **shared**  – \(can be null\) true if the contact is stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.

## Deletes the contact from the user’s contact list or the domain shared contact list

#### Syntax

```js
utils.deleteGoogleContact(contactId, shared)
```

#### Details

**contactId**  – the id of the contact.  
 **shared**  – \(can be null\) true if the contact is stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.

## Get a list of contacts from the Google Apps domain user list

#### Syntax

```js
utils.getGoogleDomainContactsFiltered(pages, maxPageResults, query, orderBy, sortOrder)
```

#### Details

**pages**  – \(can be null\) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.  
 **maxPageResults**  – \(can be null\) the max number of contacts to retrieve in every call. If null the Google default limit is used.  
 **query**  – \(can be null\) a search query. The syntax is explained in the Google Directory API documentation  
 **orderBy – ** \(can be null\) the property used to sort results  
 **sortOrder – ** \(can be null\) the sort order. Possible values are "ASCENDING" or "DESCENDING".

#### Example

fetch all users in the domain

```js
utils.getGoogleDomainContactsFiltered(null,null,null,null,null);
```

Be careful because this example may use a lot of Google API calls depending on the number of contacts. To limit the calls and data exchanged use something like:

```js
utils.getGoogleDomainContactsFiltered(3,150,’John’,’email:a*’,’DESCENDING’);
```

IMPORTANT NOTES:  
The contact may not contain an email address.



## Shared contacts synchronizations

4WS.Platform has a DB table that can contain shared contacts and can be inquired by functionalities \(grids, lookups and so on\). The table can be filled from different sources, one of which is Google Apps for Work. In particular two sources are synced:

* the Google Apps Directory, which contains the contacts of the Google Apps Domian, i.e. all people in the same domain.
* the Google Domain GAL \(Global Access List\), which contains common contacts that do not belong to the Google Domain, i.e. contacts of general interest.

  **NOTE** : The Google Apps Domain is only a source of information, not a destination. This means that the Google Apps Domain in not updated, only read.  
  To synchronize the table, each application must be configured. In case of Google Apps as source, the following parameters must be specified:

* GOOGLE\_SERVACC\_ADMIN\_USER: the account of an admin user

* GOOGLE\_SERVACC\_EMAIL: the service account email address

* GOOGLE\_SERVACC\_KEY: the service account p12 public key, Base64 encoded
* CONTACTS\_SOURCE\_GOOGLE\_DOMAIN: must contain GOOGLE keyword.

To call the synchronization method, two ways can be used:

* call the web method sharedcontactssync with a GET call on the 4WS.Platform server, for example

```js
GET http://&lt;server&gt;/sharedcontactssync
```

* use the server side Javascript call from an action:

```js
utils.sharedContatctsSync()
```

---



