The second component is used to feed a detail form by invoking tthe Alfresco API: it will get from Alfresco the metadata related to the specified document (identified by a uuid) it will pass back that content to the Platform’s detail form.
The data flow is as follow:

Platform’s Form (browser) -> Platform’s business component (Platform server) -> Alfresco CMS API layer

Both grids and forms could required input parameters to use when fetching data: a grid could require parameters to dinamically filter the grid content, the form has to pass the uuid to get a specific document. 
In both cases, a parameter is defined using the Platform syntax: :XXX, dove XXX is the parameter name.

Please do not change the business component content for a detail form: it must always contain the ID and it should never be changed.
                

---


