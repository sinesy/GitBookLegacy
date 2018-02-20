# How to get GPS coordinates

A mobile device is able to get the GPS coordinates and Platform Mobile can be configured in order to get them at any time.  
In order to do it, you have first to set enable the GPS system, when deploying the mobile app \(e.g. for iOS you have to set “usePosition” to true in the main.c file\).  
Once done that, you can fetch the GPS coordinate in a javascript action at any time, through these methods:

```js
var lat = getGPSLongitude();
var long = getGPSLatitude();
```

where both variables have String type.

---



