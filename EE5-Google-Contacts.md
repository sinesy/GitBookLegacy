With the Google contacts integration, developers can read the user contact list and retrieve data to use, for example, in Javascript actions.
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE_SERVACC_EMAIL
* GOOGLE_SERVACC_KEY

to enable the Google Apps integration and the 4WS.Platform user must be a Google Apps user.
The Javascript actions available are the following.
 **Get a list of contacts/emails from the user’s Google Apps contact list** 
## Syntax

```js
utils.getGoogleContactsFiltered(pages, maxPageResults, searchString, splitEmails)

```

## Details
 **pages**  &#8211; (can be null) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.
 **maxPageResults**  &#8211; (can be null) the max number of contacts to retrieve in every call. If null the Google default limit is used.
 **searchString**  &#8211; (can be null) a search string used for full text search on contacts.
 **splitEmails &#8211; ** (can be null) boolean value that indicates to create more contacts results in case of multiple e-mail addresses for a single contact.
## Example
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
 **Get a list of contacts/emails from the Google Apps domain shared contact list** 
## Syntax

```js
utils.getGoogleSharedContactsFiltered(pages, maxPageResults, searchString, splitEmails)

```

## Details
 **pages**  &#8211; (can be null) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.
 **maxPageResults**  &#8211; (can be null) the max number of contacts to retrieve in every call. If null the Google default limit is used.
 **searchString**  &#8211; (can be null) a search string used for full text search on shared contacts.
 **splitEmails &#8211; ** (can be null) boolean value that indicates to create more contacts results in case of multiple e-mail addresses for a single contact, .
## Example
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
Add a contact to the user’s contact list or to the domain shared contact list
## Syntax

```js
utils.addGoogleContact(name, surname, email, phone, shared)
```

## Details
 **name**  &#8211; the name of the contact.
 **surname**  &#8211; the surname of the contact.
 **email**  &#8211; the e-mail of the contact.
 **phone**  &#8211; the phone of the contact.
 **shared**  &#8211; (can be null) true if the contact must be stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.
Updates the contact of the user’s contact list or the domain shared contact list
## Syntax

```js
utils.updateGoogleContact(contactId, name, surname, email, phone, shared)
```

## Details
 **contactId**  &#8211; the id of the contact.
 **name**  &#8211; the name of the contact.
 **surname**  &#8211; the surname of the contact.
 **email**  &#8211; the e-mail of the contact.
 **phone**  &#8211; the phone of the contact.
 **shared**  &#8211; (can be null) true if the contact is stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.
Deletes the contact from the user’s contact list or the domain shared contact list
## Syntax

```js
utils.deleteGoogleContact(contactId, shared)
```

## Details
 **contactId**  &#8211; the id of the contact.
 **shared**  &#8211; (can be null) true if the contact is stored in the share contact list of the domain, false for the user’s contact list. If null, the false case applies.
Get a list of contacts from the Google Apps domain user list
## Syntax

```js
utils.getGoogleDomainContactsFiltered(pages, maxPageResults, query, orderBy, sortOrder)
```

## Details
 **pages**  &#8211; (can be null) the number of pages to retrieve. Every page is a call to Google Contacts APIs. If null all pages are retrieved.
 **maxPageResults**  &#8211; (can be null) the max number of contacts to retrieve in every call. If null the Google default limit is used.
 **query**  &#8211; (can be null) a search query. The syntax is explained in the Google Directory API documentation
 **orderBy &#8211; ** (can be null) the property used to sort results
 **sortOrder &#8211; ** (can be null) the sort order. Possible values are "ASCENDING" or "DESCENDING".
## Example
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

                

---


