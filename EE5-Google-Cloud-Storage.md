# Google Cloud Storage

4WS.Platform is integrated with Google Cloud Platform, in particular with Google Cloud Storage.  
To enable this integration a Service Account must be defined in the Google Cloud Console and the following parameters must be specified:

* GOOGLE\_SERVACC\_EMAIL: the service account email address
* GOOGLE\_SERVACC\_KEY: the service account p12 public key, Base64 encoded

The available Javascript actions are the following

## Get a signed URL

To get a signed URL for Google Cloud Storage operations \(refer to the official documentation for details: [https://cloud.google.com/storage/docs/access-control\#Signed-URLs](https://cloud.google.com/storage/docs/access-control#Signed-URLs)\).

#### Syntax

```js
utils.getGoogleCloudStorageSignedURL(verb,expiration, bucketName, objectName, mime)
```

#### Details

**verb ** – one of ‘GET’, ‘HEAD’, PUT‘’, ‘DELETE’  
 **expiration**  – This is the timestamp \(represented as the number of seconds since the Unix Epoch of 00:00:00 UTC on January 1, 1970\) when the signature expires. The server will reject any requests received after this timestamp  
 **bucketName**  – the name of the bucket which we want to operate on  
 **objectName**  – the name of the object  
 **mime**  – the MIME type of the resource. Can be null.  
_Return value_ - A string containing the signed URL.

# Get information about a bucket

#### Syntax

```js
utils.getGoogleCloudStorageBucket(bucketName)
```

#### Details

**bucketName** – the name of the bucket which we want to operate on  
_Return value_ - The file container representation \(org.wag.valueobjects.java.FileContainer\)

## Create a bucket

#### Syntax

```js
utils.createGoogleCloudBucket(project, bucketName, bucketLocation, storageClass)
```

#### Details

**project** – the id of the Google Developer Console project where the bucket must be created  
**bucketName** – the name of the bucket which we want to operate on  
**bucketLocation** – the location of the bucket. Multi-region location: US, EU, ASIA. Other locations are supported. See [https://cloud.google.com/storage/docs/](https://cloud.google.com/storage/docs/)  
**storageClass** – \(optional\) storage class: STANDARD, NEARLINE and DURABLE\_REDUCED\_AVAILABILITY. See [https://cloud.google.com/storage/](https://cloud.google.com/storage/)  
_Return value_ - the file container representation \(org.wag.valueobjects.java.FileContainer\)

## Delete a bucket

#### Syntax

```js
utils.deleteGoogleCloudStorageBucket(bucketName)
```

#### Details

**bucketName** – the name of the bucket which we want to operate on  
_Return value_ - the file container representation \(org.wag.valueobjects.java.FileContainer\)

## Enable or disable the object versioning of a bucket

#### Syntax

```js
utils.setGoogleCloudStorageBucketVersioning(bucketName,versioning)
```

#### Details

**bucketName** – the name of the bucket which we want to operate on versioning – true or false. Whether to enable or disable versioning  
_Return value_ - The file container representation \(org.wag.valueobjects.java.FileContainer\)

## Check if the object versioning of a bucket is enabled

#### **Syntax**

```js
utils.getGoogleCloudStorageBucketVersioning(bucketName)
```

#### Details

**bucketName** – the name of the bucket which we want to operate on  
_Return value_ - true or false

# Upload a file from server file system to Cloud Storage

#### Syntax

```js
utils.uploadGoogleCloudStorageObjectFromFS(fsPath, bucketName, objectName, deleteFsFile)
```

#### Details

**fsPath** – the path on the file system where the file is located  
**bucketName** – the name of the bucket which we want to upload the file to  
**objectName** – the name of the object, with the full path  
**deleteFsFile** – whether or not delete the file from file system after upload  
_Return value_ - the file representation \(org.wag.valueobjects.java.File\)

## Copy an object and its metadata to a new bucket and object destination

Can be used to copy between buckets with the same location and type. Can choose to copy from a specific object version if bucket versioning is enabled.

#### Syntax

```js
utils.copyGoogleCloudStorageObject(sourceBucketName, sourceObjectName, sourceObjectVersion, destinationBucketName, destinationObjectName)
```

#### Details

**sourceBucketName** – the bucket of the source object  
**sourceObjectName** – the source object name, with full path  
**sourceObjectVersion** – \(optional\). The object version to copy. Can be null.  
**destinationBucketName** – the destination bucket  
**destinationObjectName** – the destination object name, with full path  
_Return value_ - the file representation \(org.wag.valueobjects.java.File\)

## Copy an object and its metadata to a new bucket and object destination

Must be used to copy objects between regions and bucket types. Can choose to copy from a specific object version if bucket versioning is enabled

#### Syntax

```js
utils.rewriteGoogleCloudStorageObject(sourceBucketName, sourceObjectName, sourceObjectVersion, destinationBucketName, destinationObjectName)
```

#### Details

**sourceBucketName** – the bucket of the source object  
**sourceObjectName** – the source object name, with full path  
**sourceObjectVersion** – \(optional\). The object version to copy. Can be null.  
**destinationBucketName** – the destination bucket  
**destinationObjectName** – the destination object name, with full path  
_Return value_ - the file representation \(org.wag.valueobjects.java.File\)

## Delete an object from a bucket

#### Syntax

```js
utils.deleteGoogleCloudStorageObject(bucketName,objectName)
```

#### Details

**bucketName** – the bucket of the object  
**objectName** – the object name, with full path

## Get object information from a bucket

#### Syntax

```js
utils.getGoogleCloudStorageObject(bucketName,objectName)
```

#### Details

**bucketName** – the bucket of the object  
**objectName** – the object name, with full path  
_Return value_ - the file representation \(org.wag.valueobjects.java.File\)

## Get a list of versions of the object from a bucket

#### Syntax

```js
utils.getGoogleCloudStorageObjectVersions(bucketName,objectName)
```

#### Details

**bucketName** – the bucket of the object  
**objectName** – the object name, with full path  
_Return value_ - A list of the file version representation objects \(org.wag.valueobjects.java.FileVersion\)

## Get a list of all the objects stored in a bucket

Possibly filtered by a prefix and a delimiter. See [https://cloud.google.com/storage/docs/json\_api/v1/objects/list](https://cloud.google.com/storage/docs/json_api/v1/objects/list)

#### Syntax

```js
utils.getGoogleCloudStorageObjectVersions(bucketName,prefix,delimiter)
```

#### Details

**bucketName** – the bucket of the object  
**prefix** – the prefix to filter the objects  
**delimiter** – the path delimiter  
_Return value_ - A list of the file representation objects \(org.wag.valueobjects.java.File\)

## Get a paginated list of the objects stored in a bucket

Possibly filtered by a prefix and a delimiter. See [https://cloud.google.com/storage/docs/json\_api/v1/objects/list](https://cloud.google.com/storage/docs/json_api/v1/objects/list). The next page token can be used to retrieve more pages, maxPageResults to manage page size and pages to specify how many pages to load.

#### Syntax

```js
utils.listGoogleCloudStorageObjects(bucketName, maxPageResults, pages, nextPageToken, prefix, delimiter)
```

#### Details

**bucketName** – the bucket of the object  
**maxPageResults** – max results to load per page. Can be null  
**pages** – max pages to load. Can be null  
**nextPageToken** – the token for pagination  
**prefix** – the prefix to filter the objects  
**delimiter** – the path delimiter  
_Return value_ - A GooglePaginatedList \(org.wag.valueobjects.java.GooglePaginatedList\) of the file representation objects \(org.wag.valueobjects.java.File\)

---



