# Archiflow artifacts

The following schema describes Archiflow artifacts and how they are mapped in Platform:

| **Archiflow** | **Platform** |
| :--- | :--- |
| Document Type | Data Model |
| Fields related to a document type | Data Model fields |
| a list of cards with field values | a list of data retrieved through a server-side javascript business component and sent to a grid panel |
| a single card with field values | data retrieved through a server-side javascript business component and sent to a form panel |
| a document linked to a card | a document uploaded/downloads/previews through the Platform standard file dialog, opened starting from a grid column or form control \(having File Id type\) |



Basically, what Platform allows to do is:

* **read a list of cards**, where each field of a card is showed as a grid cell

* **download/upload/preview** a document linked to card, starting from a grid row

* **insert, update, delete cards**, through the standard grid toolbar buttons

* **read a card**, where each field of a card is showed as a form control

* **download/upload/preview** a document linked to card, starting from a specific form control

* **insert, update, delete **such a card, through the standard form toolbar buttons

* **manage programmatically all these operations**, starting from server-side javascript functions, within a server-side javascript action

---



