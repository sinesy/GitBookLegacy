# How to download a file stored remotelly

Suppose you have already stored a set of files in the Platform central site.  
This scenario requires that you have already defined a directory id, representing the path where all these files have been stored.  
You can download files in this directory from within your mobile app, by creating a javascript action. This action would be linked to some event, such as the pressing of a custom button, added to a panel.  
The action should contain something like:

```js
var filename = ...
var path = getRemoteFileURL(dirId,filename);
downloadDocument(path, filename);
```

where dirId represents the directory identifier defined on the server and filename is name of the file to fetch from the server.

---



