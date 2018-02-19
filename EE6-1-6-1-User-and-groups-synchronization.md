As part of the integration with external authenticationsystems (SSO, LDAP, AD, Google or other federated SSO systems), 4WS.Platform offers the ability to synchronize the users and/or groups from these sources.
To enable this feature the following parameters must be set in the general configuration or the application specific configuration:
 **SEC_SYNC_SOURCES** : semicolon (&#8220;;&#8221;) separated list of sources to get information from. Possible values are: GOOGLE, LDAP. Default: empty list.
 **SEC_SYNC_DESTS** :semicolon (&#8220;;&#8221;) separated list of destinationsto putinformationin. Possible values: 4WS.Default: empty list.
 **SEC_SYNC_USERS** : flag to enable or disable the synchronization of users. Possible values: "true" or "false". Default: "true".
 **SEC_SYNC_GROUPS** : flag to enable or disable the synchronization of groups. Possible values: "true" or "false". Default: "true".
To configure more than one source per type (LDAP1, LDAP2, &#8230;) use this syntax: LDAP1;LDAP2. Where LDAP1/2 is the prefix of the source.
To start the synchronization the following URL must be called:http[s]://&lt;server&gt;:&lt;port&gt;/&lt;contextroot&gt;/secursync. The call to this URL can be scheduled.
4ws.Platform synchronization
Currently 4ws.Platform is the  **destination**  of the synchronization process. The users and groups are inserted, modified, deleted (logically) and recovered (from logical delete), for every application listed in CON01 table and for every COMPANY ID-SITE ID couple specified in the configuration (see below).
To enable this synchronization specify the value **4WS** for the parameter **SEC_SYNC_DESTS** . Other parameters to specify are:
 **SYNC_4WS_COMP_SITE** : (optional) semicolon (;) separated list of COMPANY_ID,SITE_ID couples that specify company and sites for whichcreate users and groups. If not specified all the possible couples listed in PRM29_SITE_IDS are used. Example: 00888,100;00888,101;00889,10. This parameter is overloaded by the source specified company and sites (see SYNC_GOOGLE_COMP_SITE andSYNC_LDAP_COMP_SITE).
 **SYNC_4WS_DEL_USERS** : (opt. &#8211; true or false). If true delete the users from the current source before trying to write the new ones. Default: false. It is important to understand if the source list is full or incremental (only new or updated users): this depends on the sources settings. In the first case the deletion can be enabled, in the second case must be disabled.
 **SYNC_4WS_USERS_FIELDS** :(opt.) semicolon (;) separated list of 4ws.Platform user object fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields.Default value: "pk.userCodeId;description;password;;". Note: in the 4WS.Platform DB the user data is spread among different tables that PRM01_USERS; for example the mail is in SUB01 other info are in PRM08. To fill this fileds with the value from the source, specify the table prefix before the field, for example:SUB01.EMail, SUB01.firstName, SUB01.lastName. The possible values are:

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
* PRM08.languageId: string. ISO2 language code (i.e.: it, en, fr, de …)
* PRM08.userImageUrl: string. User image URL.

 ** SYNC_4WS_GROUPS_FIELDS** :(opt.) semicolon (;) separated list of 4ws.Platform groupobject fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields. Default:&#8220;pk.roleId;dictionary.description&#8221; (see Prm02Groups fields).
 **SYNC_4WS_NAME_FROM_EMAIL_FORMAT** : numeric. Code corresponding to the abilityto get name and surname from the email address, if theSUB01.eMail field is present. The currently supported codes are:
 **1**  = &lt;name&gt;.&lt;surname&gt;.&lt;other&gt;@domain
LDAP synchronization
LDAP is a source for the synchronization process. To enable this source add the **LDAP**  code to theSEC_SYNC_SOURCES parameter. This source can be used also for Active Directory synchronization.
The following parameters are needed:
 **AUTH_LDAP_SERVER** : IP address or name of the LDAP server
 **AUTH_LDAP_PORT** : (opt.) LDAP service port (default value is 389)
 **SYNC_LDAP_USERNAME** : user with read permissions on the LDAP tree, used to download users and groups.
 **SYNC_LDAP_PASSWORD** : passwordfor the user above.
 **SYNC_LDAP_PAGE_SIZE** : (opt.) download block/page size for LDAP requests. Default: 1000.
 **SYNC_LDAP_USE_PAGINATION** : (opt.) if true the pagination is used in LDAP data fetch, otherwise all data is loaded. Beware that LDAP servers can limit the pagination window. Default: true.
 **SYNC_LDAP_QUERY_SIZE_LIMIT** : (opt.) the maximum number of objects that an LDAP query fetches. Valid values start from 0 (zero &#8211; no limit), that is the default value.
 **SYNC_LDAP_COMP_SITE** : (opt.) semicolon (;) separated list of COMPANY_ID,SITE_ID couples that specify company and sites for whichcreate users and groups of this source. For different synchronization sources we could have different companies and sites. If this parameter is specified, theSYNC_4WS_COMP_SITE is overloaded, otherwiseSYNC_4WS_COMP_SITE is used. Sample value:
00888,100;00888,101;00889,10.
 **SYNC_LDAP_USER_FORM** : (opt.) format of the LDAP attribute from which extract the user name to store in 4WS.Platform. The {u} tag is the placeholder of the user name inside the format string. If not specified, theAUTH_LDAP_USER_FORM is used. If one ofAUTH_LDAP_USER_FORM orSYNC_LDAP_USER_FORM is specified, the corresponding filed type in theSYNC_LDAP_USER_TYPES parameter must be se to"UserFormatType" to apply the correct conversion. Example: {u}.mydomain.com, if the username is extracted from the e-mail address field from LDAP.
 **SYNC_LDAP_USERS_BASE** : base LDAP search path for users. Example:OU=Users,OU=Office,DC=mydomain,DC=com.
 **SYNC_LDAP_USERS_FILTER** : (opt.) filter for the users query. Useful to filter users by attribute using the LDAP syntax. Default: &#8220;(&amp;(objectclass=user)(userAccountControl:1.2.840.113556.1.4.803:=512))&#8221;. You can use this filter to get only the recently modified users using a proper condition on the filed &#8220;whenChanged&#8221;.
 **SYNC_LDAP_USERS_FIELDS** : (opt.) LDAP fields to be extracted and mapped on the sync destination for users. Default:&#8220;userPrincipalName;description;password;sn;givenName&#8221;.
 **SYNC_LDAP_USER_TYPES** : (opt.) field types, necessary to convert data, for example dates. Default:&#8220;UserFormatType;;;;&#8221;. To converto from Active Directory long type, use&#8220;ADTimestamp2Date&#8221; as data type in proper position of the list. The number of ; separated fields must be equal to the number of user fields above.
 **SYNC_LDAP_USER_KEY_ATTR** : (opt.) LDAP user object attribute to extract the user id from. Default value:&#8220;userPrincipalName&#8221;. Remember that theAUTH_LDAP_USER_FORM orSYNC_LDAP_USER_FORM parameters are used to extract the id from the field value.
 **SYNC_LDAP_USER_UNIQUE_NAME** : (opt.) unique key field among loaded LDAP user objects. It is fundamental that the value is unique. Default:&#8220;distinguishedName&#8221;.
 **SYNC_LDAP_GRPS_BASE** :base LDAP search path for groups. Example:OU=Groups,OU=Office,DC=mydomain,DC=com.
 **SYNC_LDAP_GROUPS_FILTER** : (opt.) filter for the groupsquery. Useful to filter groupsby attribute using the LDAP syntax. Default:&#8221;(objectclass=group)&#8221;
 **SYNC_LDAP_GROUPS_FIELDS** :(opt.) LDAP fields to be extracted and mapped on the sync destination for groups. Default:&#8220;cn;name&#8221;
 **SYNC_LDAP_GROUPS_TYPES** :(opt.) field types, necessary to convert data, for example dates. Default: &#8220;;&#8221;. To converto from Active Directory long type, use &#8220;ADTimestamp2Date&#8221; as data type in proper position of the list. The number of ; separated fields must be equal to the number of groupfields above.
 **SYNC_LDAP_GROUP_KEY_ATTR** :(opt.) LDAP user object attribute to extract the user id from. Default value:&#8220;cn&#8221;.
 **SYNC_LDAP_GROUP_UNIQUE_NAME** : (opt.) unique key field among loaded LDAP groupobjects. It is fundamental that the value is unique. Default:&#8220;distinguishedName&#8221;.

Note: filters on users and groups can have the form of(objectclass=user) or similar, based on object class. It is important to verify that the filter class is really used in the objects, otherwise NullPointerException errors can happen.
To specify more than one LDAP source, different from the default, call the additional source like LDAP1 and prepend &#8220;LDAP1_&#8221; to the parameters, for example:
LDAP1_SYNC_LDAP_USERNAME
LDAP1_SYNC_LDAP_PASSWORD
LDAP1_SYNC_LDAP_USERS_BASE
LDAP1_SYNC_LDAP_USERS_FILTER
LDAP1_SYNC_LDAP_USERS_FIELDS
LDAP1_SYNC_LDAP_USER_TYPES
LDAP1_SYNC_LDAP_USER_KEY_ATTR
LDAP1_SYNC_LDAP_USER_UNIQUE_NAME
LDAP1_SYNC_LDAP_GRPS_BASE
LDAP1_SYNC_LDAP_GROUPS_FILTER
LDAP1_SYNC_LDAP_GROUPS_FIELDS
LDAP1_SYNC_LDAP_GROUPS_TYPES
LDAP1_SYNC_LDAP_GROUP_KEY_ATTR
LDAP1_SYNC_LDAP_GROUP_UNIQUE_NAME
Some fixed values:
public static final String MEMBER_OF_ATTRIBUTE = &#8220;memberOf&#8221;;
public static final String MEMBER_ATTRIBUTE = &#8220;member&#8221;;
are the LDAP values from which group memberships are loaded from the user or group object.
Google Apps for Work synchronization
Google Apps for Work can be a source of users and groups, like LDAP or AD. For full explanation see this link.
                

---


