# Tree Panel

**In case of tree** , the tree definition panel is showed; through it the user has to define settings related to the tree component:

* tree title \(optional, can be hidden\)
* business component \(for list of data\) to link to the tree; the fields specified in the select clause are used to fill in nodes \(description, hidden properties\)
* tree width and height
* flags to show/hide border and to set panel opacity
* flags to allow the CRUD operations, i.e. insert, update and delete \(only if the data model linked to the selected business component is writable\); these operations are enabled only if a detail form has been associated to the current tree
* data fetching policy: when expanding a node, data for its children nodes is read; data can be retrieved in two alternative ways: using the same business component to get data \(starting from current selected node properties\) or using different business components, one for each level
* property to use for node description
* property \(optional\) to use for node icon name.

---



