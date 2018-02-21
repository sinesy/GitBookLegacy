# Client-side global variables

Client-side variables are defined and used in the web page of the web browser and they are expressed as Javascript variables. Consequently, they can be referred inside a Javascript action.  
The following table reports all available variables:

| **Variable name** | **Type** | **Example** |
| :--- | :--- | :--- |
| userRoles | Array | if \(userRoles.indexOf\("1"\)!=-1\) { // do something } |
| languageId | String | language identifier, e.g. IT, EN, … |
| appVersion | String | 4WS.Platform version, showsed in the bottom bar |
| contextPath | String | web application context path; e.g. "/platform" |
| applicationId | String | application identifier |
| userDescription | String | user description, defined in the user detail form |
| buttonsAuth | Hash table | collection of couples related to the functionalies enabled for the current logged user. Each functionality is identified by the "function id". Arrays contains 3 boolean values, related to the authorizations "can insert", "can edit", "can delete".  Authorizations are defined through the "Roles" functionality.  Example: buttonsAuth\[“contratto.gridPanel319”\] = \[true,true,true\]; |
| companyId | String | identifier of the data partition in use; 4WS.Platform supports multiple company partitions \(multi-tenancy\), where each partition is identified by the company id. |
| username | String | username of the current logged user |
| applUserPars |  | collection of couples related to tuser parameters, defined through the user detail form. |

---



