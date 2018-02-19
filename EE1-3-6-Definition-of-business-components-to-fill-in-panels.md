For every imported object \(described in the previous section\), two business components are automatically created during the importing stage:

* a business component to read a list of documents
* a business component to read a single document

## Business components for a list of documents

The first component is basically  web service: each time a grid has to show a list of documents by invoking this component, it will call the Alfresco web service layer to get the required data and it will pass back that content to the Platform’s grid.  
The data flow is as follow:

Platform’s Grid \(browser\) -&gt; Platform’s business component \(Platform server\) -&gt; Alfresco CMS Web service layer  
You are free to change the URL automatically set in that bsiness component, and add additional filter conditions, in order to define exactly the filtering logic to apply to that grid.  
See the "Examples of filtering conditions" seciton to get more details about how to set additional filters, according to the Alfresco web service syntax.

## Business component for a detail form

The second component is used to feed a detail form by invoking the Alfresco API: it will get from Alfresco the metadata related to the specified document \(identified by a uuid\) it will pass back that content to the Platform’s detail form.  
The data flow is as follow:

Platform’s Form \(browser\) -&gt; Platform’s business component \(Platform server\) -&gt; Alfresco CMS API layer

Both grids and forms could required input parameters to use when fetching data: a grid could require parameters to dinamically filter the grid content, the form has to pass the uuid to get a specific document.  
In both cases, a parameter is defined using the Platform syntax: :XXX, dove XXX is the parameter name.

Please do not change the business component content for a detail form: it must always contain the ID and it should never be changed.

## Example of filtering conditions

The second component is used to feed a detail form by invoking tthe Alfresco API: it will get from Alfresco the metadata related to the specified document \(identified by a uuid\) it will pass back that content to the Platform’s detail form.  
The data flow is as follow:

Platform’s Form \(browser\) -&gt; Platform’s business component \(Platform server\) -&gt; Alfresco CMS API layer

Both grids and forms could required input parameters to use when fetching data: a grid could require parameters to dinamically filter the grid content, the form has to pass the uuid to get a specific document.   
In both cases, a parameter is defined using the Platform syntax: :XXX, dove XXX is the parameter name.

Please do not change the business component content for a detail form: it must always contain the ID and it should never be changed.

---



