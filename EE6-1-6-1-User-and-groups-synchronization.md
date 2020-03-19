# User and groups synchronization

As part of the integration with external authenticationsystems \(SSO, LDAP, AD, Google or other federated SSO systems\), 4WS.Platform offers the ability to synchronize the users and/or groups from these sources.  
To enable this feature the following parameters must be set in the general configuration or the application specific configuration:  
 **SEC\_SYNC\_SOURCES** : semicolon \(“;”\) separated list of sources to get information from. Possible values are: GOOGLE, LDAP. Default: empty list.  
 **SEC\_SYNC\_DESTS** :semicolon \(“;”\) separated list of destinationsto putinformationin. Possible values: 4WS.Default: empty list.  
 **SEC\_SYNC\_USERS** : flag to enable or disable the synchronization of users. Possible values: "true" or "false". Default: "true".  
 **SEC\_SYNC\_GROUPS** : flag to enable or disable the synchronization of groups. Possible values: "true" or "false". Default: "true".  
To configure more than one source per type \(LDAP1, LDAP2, …\) use this syntax: LDAP1;LDAP2. Where LDAP1/2 is the prefix of the source.  
To start the synchronization the following URL must be called:http\[s\]://&lt;server&gt;:&lt;port&gt;/&lt;contextroot&gt;/secursync. The call to this URL can be scheduled.

## ** 4ws.Platform synchronization**

  
Currently 4ws.Platform is the  **destination**  of the synchronization process. The users and groups are inserted, modified, deleted \(logically\) and recovered \(from logical delete\), for every application listed in CON01 table and for every COMPANY ID-SITE ID couple specified in the configuration \(see below\).  
To enable this synchronization specify the value **4WS** for the parameter **SEC\_SYNC\_DESTS** . Other parameters to specify are:  
 **SYNC\_4WS\_COMP\_SITE** : \(optional\) semicolon \(;\) separated list of COMPANY\_ID,SITE\_ID couples that specify company and sites for whichcreate users and groups. If not specified all the possible couples listed in PRM29\_SITE\_IDS are used. Example: 00888,100;00888,101;00889,10. This parameter is overloaded by the source specified company and sites \(see SYNC\_GOOGLE\_COMP\_SITE andSYNC\_LDAP\_COMP\_SITE\).  
 **SYNC\_4WS\_DEL\_USERS** : \(opt. – true or false\). If true delete the users from the current source before trying to write the new ones. Default: false. It is important to understand if the source list is full or incremental \(only new or updated users\): this depends on the sources settings. In the first case the deletion can be enabled, in the second case must be disabled.  
 **SYNC\_4WS\_USERS\_FIELDS** :\(opt.\) semicolon \(;\) separated list of 4ws.Platform user object fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields.Default value: "pk.userCodeId;description;password;;". Note: in the 4WS.Platform DB the user data is spread among different tables that PRM01\_USERS; for example the mail is in SUB01 other info are in PRM08. To fill this fileds with the value from the source, specify the table prefix before the field, for example:SUB01.EMail, SUB01.firstName, SUB01.lastName. The possible values are:

* userInitial: string.User initials
* description: string. User description
* password: string. User password
* dateExpirationPassword: date. Password expiration date
* locked: string Y/N. Locked account
* lockDate: date. Locking date
* erasable: string Y/N. If Y the user can be deleted by the sync process
* initValidate: date. User validity starting date
* endValidate: date.User validity endingdate
* isAdmin: string Y/N. The user is admin
* SUB01.EMail: string. Email addres
* SUB01.firstName: string. Names
* SUB01.lastName: string. Surname
* SUB01.sex: tipo string M/F/O. Gender
* SUB01.address: string. Address
* SUB01.zipCode: string. ZIP code
* SUB01.city: string. City
* SUB01.country: string. Country
* SUB01.province: string. Province or state
* SUB01.birthdate: date. Birthdate
* SUB01.telephone: string.Phone number
* SUB01.mobile: string.Mobile number
* PRM08.languageId: string. ISO2 language code \(i.e.: it, en, fr, de …\)
* PRM08.userImageUrl: string. User image URL.

**SYNC\_4WS\_GROUPS\_FIELDS** :\(opt.\) semicolon \(;\) separated list of 4ws.Platform groupobject fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields. Default:“pk.roleId;dictionary.description” \(see Prm02Groups fields\).  
**SYNC\_4WS\_NAME\_FROM\_EMAIL\_FORMAT** : numeric. Code corresponding to the abilityto get name and surname from the email address, if theSUB01.eMail field is present. The currently supported codes are:  
**1**  = &lt;name&gt;.&lt;surname&gt;.&lt;other&gt;@domain

## **LDAP synchronization**

  
LDAP is a source for the synchronization process. To enable this source add the **LDAP**  code to theSEC\_SYNC\_SOURCES parameter. This source can be used also for Active Directory synchronization.  
The following parameters are needed:

* **AUTH\_LDAP\_SERVER** : IP address or name of the LDAP server
* **AUTH\_LDAP\_PORT** : \(opt.\) LDAP service port \(default value is 389\)
* **SYNC\_LDAP\_USERNAME** : user with read permissions on the LDAP tree, used to download users and groups.
* **SYNC\_LDAP\_PASSWORD** : passwordfor the user above.
* **SYNC\_LDAP\_PAGE\_SIZE** : \(opt.\) download block/page size for LDAP requests. Default: 1000.
* **SYNC\_LDAP\_USE\_PAGINATION** : \(opt.\) if true the pagination is used in LDAP data fetch, otherwise all data is loaded. Beware that LDAP servers can limit the pagination window. Default: true.
* **SYNC\_LDAP\_QUERY\_SIZE\_LIMIT** : \(opt.\) the maximum number of objects that an LDAP query fetches. Valid values start from 0 \(zero – no limit\), that is the default value.
* **SYNC\_LDAP\_COMP\_SITE** : \(opt.\) semicolon \(;\) separated list of COMPANY\_ID,SITE\_ID couples that specify company and sites for whichcreate users and groups of this source. For different synchronization sources we could have different companies and sites. If this parameter is specified, theSYNC\_4WS\_COMP\_SITE is overloaded, otherwiseSYNC\_4WS\_COMP\_SITE is used. Sample value: 00888,100;00888,101;00889,10.
* **SYNC\_LDAP\_USER\_FORM** : \(opt.\) format of the LDAP attribute from which extract the user name to store in 4WS.Platform. The {u} tag is the placeholder of the user name inside the format string. If not specified, theAUTH\_LDAP\_USER\_FORM is used. If one ofAUTH\_LDAP\_USER\_FORM orSYNC\_LDAP\_USER\_FORM is specified, the corresponding filed type in theSYNC\_LDAP\_USER\_TYPES parameter must be se to"UserFormatType" to apply the correct conversion. Example: {u}.mydomain.com, if the username is extracted from the e-mail address field from LDAP.
* **SYNC\_LDAP\_USERS\_BASE** : base LDAP search path for users. Example:OU=Users,OU=Office,DC=mydomain,DC=com.
* **SYNC\_LDAP\_USERS\_FILTER** : \(opt.\) filter for the users query. Useful to filter users by attribute using the LDAP syntax. Default: “\(&\(objectclass=user\)\(userAccountControl:1.2.840.113556.1.4.803:=512\)\)”. You can use this filter to get only the recently modified users using a proper condition on the filed “whenChanged”.
* **SYNC\_LDAP\_USERS\_FIELDS** : \(opt.\) LDAP fields to be extracted and mapped on the sync destination for users. Default:“userPrincipalName;description;password;sn;givenName”.
* **SYNC\_LDAP\_USER\_TYPES** : \(opt.\) field types, necessary to convert data, for example dates. Default:“UserFormatType;;;;”. To converto from Active Directory long type, use“ADTimestamp2Date” as data type in proper position of the list. The number of ; separated fields must be equal to the number of user fields above.
* **SYNC\_LDAP\_USER\_KEY\_ATTR** : \(opt.\) LDAP user object attribute to extract the user id from. Default value:“userPrincipalName”. Remember that theAUTH\_LDAP\_USER\_FORM orSYNC\_LDAP\_USER\_FORM parameters are used to extract the id from the field value.
* **SYNC\_LDAP\_USER\_UNIQUE\_NAME** : \(opt.\) unique key field among loaded LDAP user objects. It is fundamental that the value is unique. Default:“distinguishedName”.
* **SYNC\_LDAP\_GRPS\_BASE** :base LDAP search path for groups. Example:OU=Groups,OU=Office,DC=mydomain,DC=com.
* **SYNC\_LDAP\_GROUPS\_FILTER** : \(opt.\) filter for the groupsquery. Useful to filter groupsby attribute using the LDAP syntax. Default:”\(objectclass=group\)”
* **SYNC\_LDAP\_GROUPS\_FIELDS** :\(opt.\) LDAP fields to be extracted and mapped on the sync destination for groups. Default:“cn;name”
* **SYNC\_LDAP\_GROUPS\_TYPES** :\(opt.\) field types, necessary to convert data, for example dates. Default: “;”. To converto from Active Directory long type, use “ADTimestamp2Date” as data type in proper position of the list. The number of ; separated fields must be equal to the number of groupfields above.
* **SYNC\_LDAP\_GROUP\_KEY\_ATTR** :\(opt.\) LDAP user object attribute to extract the user id from. Default value:“cn”.
* **SYNC\_LDAP\_GROUP\_UNIQUE\_NAME** : \(opt.\) unique key field among loaded LDAP groupobjects. It is fundamental that the value is unique. Default:“distinguishedName”.

Note: filters on users and groups can have the form of\(objectclass=user\) or similar, based on object class. It is important to verify that the filter class is really used in the objects, otherwise NullPointerException errors can happen.  
To specify more than one LDAP source, different from the default, call the additional source like LDAP1 and prepend “LDAP1\_” to the parameters, for example:  
LDAP1\_SYNC\_LDAP\_USERNAME  
LDAP1\_SYNC\_LDAP\_PASSWORD  
LDAP1\_SYNC\_LDAP\_USERS\_BASE  
LDAP1\_SYNC\_LDAP\_USERS\_FILTER  
LDAP1\_SYNC\_LDAP\_USERS\_FIELDS  
LDAP1\_SYNC\_LDAP\_USER\_TYPES  
LDAP1\_SYNC\_LDAP\_USER\_KEY\_ATTR  
LDAP1\_SYNC\_LDAP\_USER\_UNIQUE\_NAME  
LDAP1\_SYNC\_LDAP\_GRPS\_BASE  
LDAP1\_SYNC\_LDAP\_GROUPS\_FILTER  
LDAP1\_SYNC\_LDAP\_GROUPS\_FIELDS  
LDAP1\_SYNC\_LDAP\_GROUPS\_TYPES  
LDAP1\_SYNC\_LDAP\_GROUP\_KEY\_ATTR  
LDAP1\_SYNC\_LDAP\_GROUP\_UNIQUE\_NAME  
Some fixed values:  
public static final String MEMBER\_OF\_ATTRIBUTE = “memberOf”;  
public static final String MEMBER\_ATTRIBUTE = “member”;  
are the LDAP values from which group memberships are loaded from the user or group object.  
Google Apps for Work synchronization  
Google Apps for Work can be a source of users and groups, like LDAP or AD. For full explanation see this link.

---



