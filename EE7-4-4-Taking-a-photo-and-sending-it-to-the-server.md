# Taking a photo and sending it to the server

A photo can be taken starting from the camera included in the mobile device.  
This task can be carried out through a javascript action to execute within the mobile device.  
The first stage is creating such an action and link to to some event, like the click event on a custom button added to a panel.  
Linking the action to some event is beyond the purpose of this section, which is focused on the content of the js action.  
The javascript content should be something like:

```js
var getPhoto = function(imagePath) {
  // do something with the image...
}
openCamera("getPhoto");
```

Basically, Platform Mobile provides a built-in method named openCamera, requiring a string argument, which is a local js function to declare before: this callback function will be automatically invoked when a photo has been taken on the mobile device.  
This callback method has an argument where the file name is passed. The file name includes the absolute path for the file in the local device.

The next step is sending such a file to the server side.  
In order to receive and store this file, a directory must be defined on the server: on the app Designer, select  **Administration -&gt; Directories -&gt; New**  and set a new directory where saving this file.  
After that, you have to define a second action, a server-side js action, which will be invoked when uploading the file to the server side: this action is helpful to execute server-side operations when receiving the file, such as saving a reference to the file name on some database table. You have to define this action, even if you don’t use it.  
In the easiest case, the callback function could contain something like:

```js
var myUploadFinishedCallback = function(responseFromWebService) {
  // do something with the response
}

var getPhoto = function(imagePath) { 
  var filePath = imagePath.substring(0,imagePath.lastIndexOf("/"));
  var fileName = imagePath.substring(imagePath.lastIndexOf("/")+1);

  var url = getBaseURL() + "/executeJs/uploadfiles?appId=...&amp;applicationId=...&amp;actionId=...&amp;dirId=...&amp;unzip=false&amp;restfulToken="+getToken();
  sendFile(url,filePath, fileName, "myUploadFinishedCallback");

}
```

where a few parameters are required:

* appId/applicationId: the application id for the current mobile app
* actionId: the id for the server-side js action
* dirId: the directory id defined previously
* imagePath: the absolute path + file name passed to the callback function
* myCallback: the name of a second local function, which will be invoked after the upload process has been completed. You could leave it empty if you don’t need any custom logic after sending the file.

---



