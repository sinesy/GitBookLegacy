# Mobile Introduction

The 4WS.Platform – Mobile edition can operate with iOS and Android devices, both on tablet and smartphones.  
Any number of mobile apps can be created starting from a single installation of Platform.  
This solution is composed of:  
a ** server-side Platform installation** , containing the Enterprise Mobile module able to communicate with the Platform Mobile apps  
a  **mobile app** , which consists of an interpreter created once for iOS and Android, which communicates with the server side to receive the metadata needed to define the behavior of the app \(both GUI, business logic and data structures\). Once received this metadata, the app is ready to work and can synchronize with the server side to invoke web services, send or receive data and files.

![](http://4wsplatform.org/wp-content/uploads/2018/01/mobilearch-1024x576.png)

**Cross features**

* on-line apps \(app connected to a server to manage data, through an Internet connection\)
* off-line apps \(data managed locally, without an Internet connection\)
* authentication or user authentication
* user authorizations \(different menu according to the user, different operations according to the user\)
* data synchronization filtered per user
* file synchronization

**UI features**

* menus: slide menu, icons menu, tabs
* layout support: border, card
* filter panels
* read-only grids with sorting support, data pagination, connection with filter panel
* grids with embedded forms
* forms \(data loading and saving\)
* editable panels \(no data loading, data edited on-the-fly\)
* code selectors, buttons, links, labels, input controls
* image gallery
* google map \(on-line feature\)
* google chart panel \(on-line feature\)
* preview panel \(PDFs, images, etc.\) with upload/download/preview support
* integration with camera and device image gallery
* \(clickable\) web view
* app messages based on dialogs or toasts
* customizations: theme, menu type, custom code based on Javascript

**Integration features**

* device file system management
* device SqlLite database management
* push notifications based on Firebase
* social media integration \(Facebook login and posts, Google+, etc.\)
* barcode scanning
* Estimote eBeacons support

---



