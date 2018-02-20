# Google Drive

With this integration, developers can automate the upload, download, update and deletion of files in the user’s Google Drive space. This feature is not intended for Google Drive UI substitution, but for basic and automatic operations and processes.  
 **NOTE: ** currently the Google Drive APIs v2 are supported \(see documentation\).  
In order to use this feature, you have also to define a few parameters in 4WS.Platform:

* GOOGLE\_SERVACC\_EMAIL
* GOOGLE\_SERVACC\_KEY

to enable the Google Apps integration, and the 4WS.Platform user must be a Google Apps user.  
4WS.Platform file model  
Files and folders are represented in 4WS.Platform by the class org.wag.valueobjects.java.File. Objects of that class are converted to Javascript when used as return values of the server side Javascript actions \(see below\).  
The attributes of the class are:

* String  **id** ;
* String  **title** ;
* String  **description** ;
* Long  **size** ;
* String  **mimeType** ;
* String  **path** ;
* String  **pathType** ;
* String  **iconPath** ;
* String  **iconPathType** ;
* boolean  **folder** ;

Javascript actions  
These are the available Javascript actions.  
 **NOTE: almost every method has two versions. One that uses the current logged user to access Google Drive and one that let to specify the userId to access a different Google Drive account.**

## Get information about a file stored in Google Drive

#### Syntax

```js
utils.getGoogleDriveFileInfo(userId, fileId)

utils.getGoogleDriveFileInfo(fileId)
```

#### Details

**fileId**  – the id of the file  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\).

#### Example

this example shows how to call the method from a Javascript Server action and get the title of the file. The full list of fields can be found in the Java org.wag.valueobjects.java.File class.

```js
var file = utils.getGoogleDriveFileInfo('');

utils.setReturnValue('{ "name":"' + file.title +'" }');
```

After this we can use the information obtained.  
If the return value of the server call is needed on the client side, a Javascript client call can be set up to get the JSON object representing, in this case, the id \(the actionId is the id of the Javascript Server action\):

```js
var resp = new SyncRequest().send(
   contextPath+"/executeJs?applicationId=&lt;appId&gt;" +
   "&amp;actionId=&lt;actionId&gt;",
   "POST",
   null
);
var file = Ext.decode(resp);
showMessageDialog('Message',Title is ' + file.name, null, true);
```

## Upload a file in Google Drive from the server file system

#### Syntax

```js
utils.uploadGoogleDriveFileFromFS(userId, fsPath, parentId, deleteFsFile)

utils.uploadAndRenameGoogleDriveFileFromFS(userId, fsPath, parentId, fileName, deleteFsFile)

utils.uploadGoogleDriveFileFromFS(fsPath, parentId, deleteFsFile)

utils.uploadAndRenameGoogleDriveFileFromFS(fsPath, parentId, fileName, deleteFsFile)
```

#### Details

**fsPath**  – the full path of the file to upload. This path is in the server where 4WS.Platform is installed.  
 **parentId**  – the id of the Drive folder where the file must be uploaded to. Can be null, in this case the root folder is used.  
 **fileName**  – the new name of the uploaded file. If null the original file name is used.  
 **deleteFsFile ** – true or false. Specifies if the file on file system must be deleted or not after upload to Drive.  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\).

#### Example

This example shows how to call the method from a Javascript Server action and get the file object. The full list of fields can be found in the Java org.wag.valueobjects.java.File class.

```js
var file = utils.uploadGoogleDriveFileFromFS('', null, false);
```

## Update a file in Google Drive

The file source is in the server file system. This creates a new version of the file in Google Drive.

#### Syntax

```js
utils.updateGoogleDriveFileFromFS(userId, fileId, fsPath, deleteFsFile, newRevision)

utils.updateGoogleDriveFileFromFS(fileId, fsPath, deleteFsFile, newRevision)
```

#### Details

**fileId ** – the id of the file to update  
 **fsPath**  – the full path of the file to upload. This path is in the server where 4WS.Platform is installed.  
 **deleteFsFile ** – true or false. Specifies if the file on file system must be deleted or not after upload to Drive.  
 **fileName**  – the new name of the uploaded file. If null the original file name is used.  
 **newRevision ** – true or false. Specifies if a new revision must be created or the file must be overwritten.  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\).

#### Example

This example shows how to call the method from a Javascript Server action and get the file object. The full list of fields can be found in the Java org.wag.valueobjects.java.File class.

```js
var file = utils.updateGoogleDriveFileFromFS('','',false);

utils.setReturnValue('{ "name":"' + file.title +'" }');
```

## Upload a file in Google Drive

In a folder with a specific name, contained in a base folder with a specific id. If the folder with the name does not exist in the base folder, it can be created or not:

#### Syntax

```js
utils.uploadGoogleDriveFileInNamedFolderFromFS(userId, fsPath, baseFolderId, folderName, createFolderIfNotExists, deleteFsFile)

utils.uploadAndRenameGoogleDriveFileInNamedFolderFromFS(userId, fsPath, baseFolderId, folderName, createFolderIfNotExists, fileName, deleteFsFile)

utils.uploadGoogleDriveFileInNamedFolderFromFS(fsPath, baseFolderId, folderName, createFolderIfNotExists, deleteFsFile)

utils.uploadAndRenameGoogleDriveFileInNamedFolderFromFS(fsPath, baseFolderId, folderName, createFolderIfNotExists, fileName, deleteFsFile)
```

#### Details

**fsPath**  – the full path of the file to upload. This path is in the server where 4WS.Platform is installed.  
 **baseFolderId**  – the id of the Drive folder where the named folder must be created.  
 **folderName ** – a name of the folder where the file must be uploaded to. This folder must be in the base folder  
 **createFolderIfNotExists ** – true or false. Whether or not to create the  **folderName**  folder if not exists in the base folder  
 **fileName**  – the new name of the uploaded file. If null the original file name is used.  
 **deleteFsFile ** – true or false. Specifies if the file on file system must be deleted or not after upload to Drive.  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\).

## Move a file or folder in a single folder

If in the destination folder exists a single file with the same title/name of the file to move, different results happen depending on the addToRevision value:

if false, the file is moved under the new single folder and the homonymous file is kept as is. Two files with the same name will be present in the folder.  
if true, the file is saved as a new history version of the homonymous file in the destination folder, and deleted

#### **Syntax**

```js
utils.moveGoogleDriveFile(userId, fileId, newParents,addToRevision)

utils.moveGoogleDriveFile(fileId, newParents,addToRevision)
```

#### **Details**

**fileId** – the id of the file/folder to move  
**newParents** – a comma separated list of folder ids that will become the new parents of the file/folder.  
**addToRevision** – true/false. If true the file will be new version of a possible homonymous file in the destination folder. If false two files with the same name will be present in the destination folder.

#### **Example**

This example shows how to call the method from a Javascript Server action and get the file object. The full list of fields can be found in the Java File class.  
`var file = utils.moveGoogleDriveFile(‘<file_id>’,'<new_folder_id>’,true);          
 utils.setReturnValue(‘{ “name”:”‘ + file.title +'” }’);`

## Move a file or folder

You can specify a list of comma separated folder ids to become the parents of the file/folder. The current parents are removed.

#### Syntax

```js
utils.moveGoogleDriveFile(userId, fileId, newParents)

utils.moveGoogleDriveFile(fileId, newParents)
```

#### Details

**fileId** – the id of the file/folder to move  
**newParents** – a comma separated list of folder ids that will become the new parents of the file/folder.

#### Example

This example shows how to call the method from a Javascript Server action and get the file object. The full list of fields can be found in the Java File class.

```js
var file = utils.moveGoogleDriveFile('&lt;file_id&gt;','&lt;new_folder_id&gt;');

utils.setReturnValue('{ "name":"' + file.title +'" }');
```

## Modify the parents of a file or folder

You can specify a list of comma separated folder ids to add as parents of the file/folder and a list of parents to remove.

#### Syntax

```js
utils.modifyGoogleDriveFileParents(userId, fileId, parentsToAdd, parentsToRemove)

utils.modifyGoogleDriveFileParents(fileId, parentsToAdd, parentsToRemove)
```

#### Details

**fileId** – the id of the file/folder to patch  
**parentsToAdd** – a comma separated list of folder ids that will be added as parents of the file/folder. Can be empty.  
**parentsToAdd** – a comma separated list of folder ids that will be removed as parents of the file/folder. Can be empty.

#### Example

This example shows how to call the method from a Javascript Server action and get the file object. The full list of fields can be found in the Java File class.

```js
var file = utils.moveGoogleDriveFile('&lt;file_id&gt;', '&lt;add_folder_id_1&gt;,&lt;add_folder_id_2&gt;', '&lt;remove_folder_id_1&gt;,&lt;remove_folder_id_2&gt;');
utils.setReturnValue('{ "name":"' + file.title +'" }');
```

## Delete a file or folder from Google Drive

You can specify if move the file in the trash or delete it immediately.

#### Syntax

```js
utils.deleteGoogleDriveFile(userId, fileId, skipTrash)

utils.deleteGoogleDriveFile(fileId, skipTrash)
```

#### Details

**fileId ** – the id of the file to delete  
 **skipTrash ** – true or false. Specifies if the file is deleted immediately or moved to trash.

#### Example

This example shows how to call the method from a Javascript Server action and get the file object.The full list of fields can be found in the Java org.wag.valueobjects.java.File class.

```js
var file = utils.deleteGoogleDriveFile('',false);

utils.setReturnValue('{ "name":"' + file.title +'" }');
```

## Recover a file or folder from Google Drive trash

#### Syntax

```js
utils.recoverGoogleDriveFile(userId, fileId)

utils.recoverGoogleDriveFile(fileId)
```

#### Details

**fileId ** – the id of the file to restore from trash  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\).

#### Example

this example shows how to call the method from a Javascript Server action and get the file object.The full list of fields can be found in the Java org.wag.valueobjects.java.File class.

```js
var file = utils.recoverGoogleDriveFile('');

utils.setReturnValue('{ "name":"' + file.title +'" }');
```

## Return the URL to open a file from Google Drive

This URL should be opened in a browser and must be used for files in Google Drive format \(documents, spreadsheets, presentations, forms and so on\).

#### Syntax

```js
utils.getGoogleDriveFileOpenURL(fileId)
```

#### Details

**fileId ** – the id of the file  
_Return value_ - a string containing the URL

## Return the URL to download a file from Google Drive

This must be used for uploaded files \(PDF, JPG, PNG, DOCX, XSLX, PPTX, TXT and so on\).

#### Syntax

```js
utils.getGoogleDriveFileDownloadURL(fileId)
```

#### Details

**fileId ** – the id of the file  
_Return value_ - a string containing the URL

## Get the stored versions of the given file

For both Google and non Google formats.

#### Syntax

```js
utils.getGoogleDriveFileRevisions(fileId)
```

#### Details

**fileId ** – the id of the file  
_Return value_ - a list of the Platform representation of the version of a file \(List\)

## Create a folder in Google Drive with the specified parents and optional description

#### Syntax

```js
utils.createGoogleDriveFolder(userId, folderName, parents, description)

utils.createGoogleDriveFolder(folderName, parents, description)
```

#### Details

**folderName ** – the name of the folder  
 **parents**  – a list of ids of parent folders. In general one folder.  
 **description**  – an optional description of the folder  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\) having the boolean flag "folder" with true value.

## Return a list of ids of files/folder that are children of the specified folder

#### Syntax

```js
utils.getGoogleDriveFolderContentsIds(userId, folderId, query, trashed)

utils.getGoogleDriveFolderContentsIds(folderId, query, trashed)
```

#### Details

**folderId ** – the id of the folder  
 **query**  – an optional query to filter the search \(see docs\)  
 **trashed**  – true or false. Specify if extact also trashed files/folders.  
_Return value_ - list of strings

## Return a list of files/folder that are children of the specified folder

#### Syntax

```js
utils.getGoogleDriveFolderContents(userId, folderId, query, trashed)

utils.getGoogleDriveFolderContents(folderId, query, trashed)
```

#### Details

**folderId ** – the id of the folder  
 **query**  – an optional query to filter the search \(see docs\)  
 **trashed**  – true or false. Specify if extact also trashed files/folders.  
_Return value_ - list of the Platform file representation \(org.wag.valueobjects.java.File\)

## Set the permissions for a file/folder

#### Syntax

```js
utils.setGoogleDriveFilePermissions(userId, fileId, type, value, role, additionalRoles, sendNotifications, message)

utils.setGoogleDriveFilePermissions(fileId, type, value, role, additionalRoles, sendNotifications, message)
```

#### Details

**fileId ** – the id of the file/folder  
 **type ** – the type of sharing, one between “user”, “group”, “domain” or “default”  
 **value**  – the email of the user/group or the domain name  
 **role**  – the role one of “reader”, “writer” or “owner”  
 **additionalRoles**  – optional string, for example “commenter”  
 **sendNotifications**  – true or false. Specify if send the notification to the user/group specified in the value.  
 **message**  – optional message for the notification

## Set additional attributes of a file/folder

#### Syntax

```js
utils.setGoogleDriveFileAttributes(userId, fileId, fileAttributes)

utils.setGoogleDriveFileAttributes(fileId, fileAttributes)
```

#### Details

**fileId**  – the id of the file/folder  
 **fileAttributes**  – the attributes as defined in org.wag.valueobjects.java.FileAttributes. Currently: starred, trashed, restricted, viewed, writersCanShare.

## Tree duplication

Duplicates the folder  **sourceFolderId**  and all its contents in a folder called  **newFolderName**  with optional description  **newFolderDescription**  under folder  **destinationFolderId** . It is also possible to specify a  **titlePrefix ** to prepend to the title of every duplicated resource \(files or folders\) and whether or not  **copyPermissions**  from the original folder to the duplicated forlder.

#### Syntax

```js
utils.duplicateGoogleDriveFolderAndContents(userId, sourceFolderId, newFolderName, newFolderDescription, destinationFolderId, titlePrefix, copyPermissions)

utils.duplicateGoogleDriveFolderAndContents(sourceFolderId, newFolderName, newFolderDescription, destinationFolderId, titlePrefix, copyPermissions)
```

#### Details

**sourceFolderId ** – the id of the original folder  
 **newFolderName**  – the name of the copy of the folder  
 **newFolderDescription ** – optional description for the new folder  
 **destinationFolderId ** – the id of the folder where the copy must be created. Can be "root" for the root drive folder.  
 **titlePrefix**  – a prefix  
 **copyPermissions**  – true or false. Copy the permissions of the original folder in the duplicate folder.  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\) having the boolean flag "folder" with true value.

## Tree permissions

Adds a single permission to a folder and its contents. It is possible to specify a role for files and a role for folders \(for example to make folders read only and files read/write\). additionlRoles**  lets to specify the “commenter” role or other future capabilities. recursive**  lets to go deep in the folder tree, otherwise it stops on the first level inside folderId\*\* . Notifications with a message can be sent for every resource.

#### Syntax

```js
utils.addPermissionsToGoogleDriveFolder(userId, folderId, type, value, fileRole, folderRole, additionalRoles, updateBaseFolder, recursive, sendNotifications, message)

utils.addPermissionsToGoogleDriveFolder(folderId, type, value, fileRole, folderRole, additionalRoles, updateBaseFolder, recursive, sendNotifications, message)
```

#### Details

**folderId ** – the id of the original folder  
 **type ** – the type of sharing, one between "user", "group", "domain" or "default"  
 **value**  – the email of the user/group or the domain name  
 **fileRole**  – the role for files, one of "reader", "writer" or "owner"  
 **folderRole**  – the role for folders, one of "reader", "writer" or "ownerv  
 **additionalRoles**  – optional string, for example "commenter"  
 **updateBaseFolder**  – true or false. If true applies permissions to the base folder identified by folderId.  
 **recursive**  – true or false. If true applies permissions to all subtree, otherwise only to the first level.  
 **sendNotifications**  – true or false. Specify if send the notification to the user/group specified in the value.  
 **message**  – optional message for the notification.  
_Return value_ - the Platform file representation \(org.wag.valueobjects.java.File\) having the boolean flag "folder" with true value.

## Return the value of a property for the specified file and visibility

#### Syntax

```js
utils.getGoogleDriveFileProperty(userId, fileId, key, visibility)

utils.getGoogleDriveFileProperty(fileId, key, visibility)
```

#### Details

**fileId ** – the id of the file/folder  
 **key ** – the key of the property to get  
 **visibility**  – "PRIVATE" or "PUBLIC"  
_Return value_ - a String containing the property value.

## Add property for the specified file and visibility

#### Syntax

```js
utils.addGoogleDriveFileProperty(userId, fileId, key, value, visibility)

utils.addGoogleDriveFileProperty(fileId, key, value, visibility)
```

#### Details

**fileId ** – the id of the file/folder  
 **key ** – the key of the property to get  
 **value**  – the value  
 **visibility**  – "PRIVATE" or "PUBLIC"

## Patches a property for the specified file and visibility

#### Syntax

```js
utils.patchGoogleDriveFileProperty(userId, fileId, key, value, visibility)

utils.patchGoogleDriveFileProperty(fileId, key, value, visibility)
```

#### Details

**fileId ** – the id of the file/folder  
 **key ** – the key of the property to get  
 **value**  – the value  
 **visibility**  – "PRIVATE" or "PUBLIC"

## Patches a property for the specified file

#### Syntax

```js
utils.deleteGoogleDriveFileProperty(userId, fileId, key)

utils.deleteGoogleDriveFileProperty(fileId, key)
```

#### Details

**fileId ** – the id of the file/folder  
 **key ** – the key of the property to get

---



