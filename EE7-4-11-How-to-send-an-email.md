# How to send and email

Emails can only be sent from the server-side of Platform, not from the mobile device.  
In order to send emails, you have first to configure a few application parameters, that you can set by opening: Application -&gt; Application Detail -&gt; folder Application Parameters -&gt; section “Mail”. Here you have to fill the required parameters to connect to an SMTP server.  
Once done that, you are allowed to send emails, starting from a server-side javascript action.  
Such action could contain something like:

```js
var response = {
    success: true,
    message: ""
};
try{
    var destinationAddress = vo.destinationAddress;
    var senderAddress = vo.senderAddress;
    var subject = vo.subject;
    var body = vo.body;
    var fileToAttach = vo.fileToAttach;
    var dirId = vo.dirId;

    var path = utils.getDirectoryPath(parseInt(dirId)) + "/" + fileToAttach;
    utils.sendEmail(senderAddress, destinationAddress, "", "", subject, body, false, false, false, false, [path]);
    response.message = "OK";
    utils.log("Email sent.", "WARN");
}catch(e){
    response.success = false;
    response.message = e.message;
    utils.log("ERROR: " + e.message, "ERROR");
}
utils.setReturnValue(JSON.stringify(response));
```

This is just an example of a sort of action used to sent emails. This example requires to be invoked using a POST HTTP method and a request body expressed in JSON format having the following content:

```js
{
 destinationAddress: "...",
 senderAddress: "...",
 subject: "...",
 body: "...",
 fileToAttach: "...",
 dirId: "..."
}
```

Of course you have not to pass all these data if you prefer to hard-coded part of it within the action: it is up to you what to pass to the action from the mobile app.  
In the example above, you can even attach a file to the email message: this file must be previously saved on the server in some way and here it is simply referred starting from its name and the directory id representing the location where it has been saved.

On the mobile side, you have to define a javascript action, invoked starting from some event \(e.g. a button click\) and use it to invoke the server-side javascript action.

## Example

```js
var url = 
  getBaseURL()+
  '/executeJs?'+
  'applicationId=...&amp;appId=...&amp;'+
  'actionId=...'+
  'restfulToken='+getToken();

var obj = { destinationAddress: "...",  senderAddress: "...",  subject: "...",  body: "...",  fileToAttach: "...",  dirId: "..." };

var jsonRequest = JSON.stringify(obj);

var jsonResponse = getWebContent(url,"POST","application/json",jsonRequest);
var response = eval("("+jsonResponse+")");
```

---



