# Server global variables

Server-side variables are defined and used on the server side actions, i.e. on SQL type actions and Server-side Javascript actions.  
Variables can be referred on SQL actions using a double period + an upper-case expression \(e.g. :USERNAME, :LANGUAGE\_ID, etc.\).  
Variables can be expressed in Server-side Javascript acitons using the "camel mode"-like variabes \(e.g. username, languageId, etc.\). The variables of the request are available in the object “reqParams” \(e.g.: reqParams.applicationId etc\)

The following table reports all available variables:

| **Variable name** | **Type** | **Example** |
| :--- | :--- | :--- |
| USERNAME | String | username of the current logged user |
| LANGUAGE\_ID | String | language identifier, e.g. IT, EN, … |
| COMPANY\_ID | String | identifier of the data partition in use; 4WS.Platform supports multiple company partitions \(multi-tenancy\), where each partition is identified by the company id. |
| SITE\_ID | Number | code used to filter data |
| TODAY | String | current date |
| MONTH | Number | Month of the year, expressed as0..11 \(jan..dec\) |
| DAY | Number | Day of the month |
| DOW | Number | day of the week, expressed as 0..6 \(sun-sat\) |
| NOW | Date | Current date+time |
| APPLICATION\_ID | String | application identifier |

---



