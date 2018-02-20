# Setting up the environment

In order to connect to Google Datastore, you have to get a Google Account and you have to set up all required parameters in order to connect to a specific datastore name \(dataset id\).  
These are the global parameters to set:

* Google Service Account Email
* Google Apps domain admin user for Google Service Account access \(email\)
* Google Service Account Key \(p12 key Base64 encoded\)
* Dataset id – basically it is the Google Cloud Project Id

You can get the first 3 parameters by accessing the Google Admin console, choose “API Management” -&gt; “Credentials” -&gt; “Service Account Keys” -&gt; “Manage Service Account Keys”.  
You have to use an online web service to convert the binary account key to the Base64 format \(p12 key\).  
Since you have specified the dataset id per Google Cloud Project, every Datastore entity you define can be accessed by any application pointing to that project.

Once done that, you can start creating entities, defining enquiries using the GQL query language, creating panels connected to these components and manage all reading and writing operations involved with the panes.

---



