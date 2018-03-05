# Creating a mobile app common use cases

#### **Opening a detail form in a window, starting from a click in a row of a grid** {#opendetailform}

Suppose you have a window containing a grid and you want to replace that window with a window containing a detail form where showing data related to a row selected in grid.  
The steps to follow are:

1. create the Data Model for grid and form
2. create or redefine the “Business Component for a list” to link to the grid
3. create or redefine the “Business Component for a form” to link to the form and be sure to include in the WHERE clause a filtering condition to read one only record \(e.g. WHERE MY\_TABLE.MY\_PK = :MY\_PK\)
4. create a window containing the grid, using UI -&gt; Windows -&gt; New window an choose the grid panel option
5. create a window containing the detail form, using UI -&gt; Windows -&gt; New window an choose the detail form option
6. open the window containing the grid, select the Panels subfolder and open the corresponding grid \(right click on the tree node related to the grid and then select “Show panl details”
7. choose the Events subfolder in the grid panel definition window and add a new event having type “Touch event on a grid row”
8. double click on the Action cell to open the Action editor
9. in the Action editor, select the “Javascript” option and type the following code:

```js
var args = new Object();
args.myPk=vo.myPk;
openWindowXXX(args);
```

where XXX represents the id for the window containing the form panel.  
Basically, through this code, you are passing the myPk attribute \(corresponding to the physical database field MY\_PK\) from the grid’s row to the window to open.  
The variable “args” represents any number of attributes to pass forward to the window to open.  
 **Note** : Everything described here can be automated using the Windows -&gt; New window wizard and choose a form directly connected to the grid, i.e. when defining the form, select the “Linked grid” combobox.

#### **Opening a report in a window** {#openreport}

PDF documents cab ne generated on the fly only on the web side, but the can be showed in a window of the mobile app.  
Consequently, you always need to have a working Internet connection in order to invoke the reports generation, download it and then show it within the app.  
Reports can be generated using Jasper Report, which is embedded in the web layer.  
The report execution can be started using a javascript action. You can link that action in any point of your app.  
Typical scanarios are:

* create a custom button in a grid or form \(shown in the topbar\) and link to its click the execution of the action

* listen for the row click in a grid and link to that event the execution of the action

* create a menu item having javascript type, i.e. directly linked to the action

Independently of the event listened to, the action should contain something like the following:

```js
var url = getBaseURL()+"/reports/getReport?applicationId=XXX&amp;appId=XXX&amp;reportName=reports/myreport.jasper&amp;datastoreId=YYY&amp;reportFormat=PDF&amp;restfulToken="+getToken();
var json = getWebContent(url,"GET","application/json",null);
var response = eval("("+json+")");
if (response.success) {
    var title = "Report.pdf";
    var url = 
      getBaseURL()+'/showDocument?'+
      'applicationId=XXX&amp;title='+title+
      '&amp;docId='+response.data.docId+
      '&amp;exportFormat='+response.data.exportFormat+
      '&amp;restfulToken='+getToken();

    openRemoteDocument(title,url);
}
```

where:

* XXX represents the application id for your mobile app
* myreport.jasper is an example of a Jasper Report template file, which must be uploaded in a subfolder named “reports” of your application context. In order to do it, you can use the Administration -&gt; File Manager feature and upload a zip file containing the “reports” subfolder and the .jasper file inside it, as well as any other depending file \(images, sub reports…\), once uploaded it, the .zip file will be automatically decompressed and you will see the .jasper file correctly stored in the “reports” subfolder
* YYY is the datastore id, that you have to define on the server side, related to the database schema where the .jasper file has to work with

That’s all!

#### **Choosing a photo from photo-library/take a photo and send it to the server** {#sendingphototoserver}

Platform provides a series of javascript methods you can use to manage photos.  
What you need to to is creating a javascript action and include in it a few built-in methods:

```js
var uploadImageCallback = function(responseT) {

}

var photoCallback = function(fileName){ 
        if(fileName != null){        
          // do something with the file...
          // ...

          // upload the file to the server side...
          sendFile(url, fileName, newfilename.jpg"", "uploadImageCallback");   
        }
}

openCamera("photoCallback");
```

**openCamera**  is a built-in method you can use to open the mobile camera and take a photo. The required argument is the name of a javascript function you have to include in the same action. This is the callback action that will be invoked when the end user will choose/take a photo.  
In this example, the callback function is named “photoCallback” and it must have one argument: the filename. This is filled by the mobile app with the absolute path \(including the file name\) of the image stored locally in the app file system.  
If it is filled, you can work with it. For example, you could resize the image, with another utility method named  **resizeAndSaveImage** , provided by Platform:

```js
var quality = 0.8;
var width = 800;
var height = 1200;
var resizeFile = fileName.substr(0, fileName.lastIndexOf(".")) + ".jpg";
resizeAndSaveImage(quality, width, height, fileName, resizeFile);
fileName = resizeFile; 
fileName = fileName.replace("file:///", "");
```

You can send the file to the server side, using the other built-in method called  **sendFile** , which requires a few arguments:

* the server-side URL to invoke
* the filename related to the local file to send
* the new filename it will have on the server-side
* the function name, defined in the same action, which will be automatically invoked when the file upload process has been successfully completed

The URL to define could be something like:

```js
var url = getBaseURL() + "/executeJs/uploadfile?appId=XXX&amp;applicationId=XXX&amp;actionId=YYY&amp;dirId=ZZZ&amp;unzip=false&amp;restfulToken=" + getToken(); // + other parameters, if needed
```

where:

* XXX is the application id
* YYY is the action id to define on the server \(a server-side javascript action\), which will be automatically invoked just after receiving the file. This is helpful to carry out additional operations on the server, like saving a record in a table, related to the file just received form the mobile app
* ZZZ is the directory id, i.e. the identifier of a directory defined through Administration -&gt; Directories: it represents the path where the file just received will be stored

#### **Scanning a barcode using the camera** {#scanningbarcode}

Platform provides a built-in method to scan a barcode:

```js
var callbackSuccess = function (barcodeContent){ 
    var barcodeObj = JSON.parse(barcodeContent); 
    var barcode = barcodeObj.rawValue;
    // ...
};  

var callbackCancel = function (){ 
    var opts = new Object(); 
    opts['title'] = "QRCode"; 
    opts['subtitle'] = 'Operation cancel by the user'; 
    opts['titleButtonSuccess'] = 'OK'; 
    showMessageDialog(opts, null); 
}; 

var callbackError = function (errorMessage){ 
    var opts = new Object(); 
    opts['title'] = "QRCode"; 
    opts['subtitle'] = errorMessage; 
    opts['titleButtonSuccess'] = 'OK'; 
    showMessageDialog(opts, null); 
}; 

scanBarcode("callbackSuccess", "callbackCancel", "callbackError");
```

The  **scanBarcode**  method is used to start the scanning process.Three arguments are required:

* a function name, related to a javascript function to define in the same action, which will be invoked if the scanning process worked correctly and a bar code has been retrieved
* a function name, related to a javascript function to define in the same action, which will be invoked if the scanning process has been interrupted by the end user
* a function name, related to a javascript function to define in the same action, which will be invoked if the scanning process was interrupted with an error

The first callback requires an argument, which is a javascript object containing the barcode text value.  
The third callbackrequires an argument, which is the error message optionally to show in a window.

---



