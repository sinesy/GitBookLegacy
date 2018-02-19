The first component is basically  web service: each time a grid has to show a list of documents by invoking this component, it will call the Alfresco web service layer to get the required data and it will pass back that content to the Platform’s grid.
The data flow is as follow:

Platform’s Grid (browser) -> Platform’s business component (Platform server) -> Alfresco CMS Web service layer
You are free to change the URL automatically set in that bsiness component, and add additional filter conditions, in order to define exactly the filtering logic to apply to that grid.
See the "Examples of filtering conditions" seciton to get more details about how to set additional filters, according to the Alfresco web service syntax.


                

---


