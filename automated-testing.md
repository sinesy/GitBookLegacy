# Automated Testing

Platform allows to quickly create a large portion of your application, using the wizards it provides. Thanks to them, the generated part of application is likely to work perfectly, unless your business logic \(SQL layer\) has been defined wrongly.

Apart from that, there is  another layer which can be considered critical from a quality point of view: server-side custom logic, written using javascript.

This part should be limited as possible but most of applications include a small part which is so custom that can be realized only using a programming language, which is Javascript in case of Platform.

You can create as many server-side javascript actions as you want. These actions represent a web service layer which can be invoked either by your web GUI, a mobile App or an external application.

In any case, the problem involved with this source code is that it should be tested.

Platform provides a module to quickly create Test Cases, i.e. HTTP requests you can use to invoke to call and test your web services \(your server-side actions\). It also allows to define testing conditions, in order to check out whether the response of the web service is the one expected.

This feature allows you to define:

* HTTP method
* HTTP request URL
* query parameters \(i.e. parameters included in the URL, after the ?\)
* header parameters
* BODY content

As well as testing conditions on the response of the web service invokation.

Outcomes are also automatically saved in Platform Table Log feature, so that you can monitor the progress of the test results over time and collect an history of these executions.



### How to create a Test Case manually

This feature can be accessed through the App Designer menubar: **Services -&gt; Automated Tests**

![](/assets/test-main.png)

You can create as many Test Cases as you want. They are reported in the list on the left, filtered by **collection**. On top of this list there is a combo-box you can use to filter Tests Cases by collection. If not specified, all Tests Cases are reported.

The main part of the window is about the detail of the selected Test Case.

You can **create a new Test Case** by pressing the **New** button on top of the list.

![](/assets/test-new.png)

Here you have to specify:

* a **name** for the Test Case \(mandatory\)
* a **collection** it belongs to \(mandatory\); this editable combo-box allows you to choose an already existing collection or simply digit it for the first time
* the **HTTP request** \(mandatory\), in terms of HTTP method and URL; here you can specify any number of variables, always expressed as {{VARNAME}}
* an optional **action** \(web service\), used to link many Test Cases to the same action; this setting does not have any real usage, expect for grouping many Test Cases to a specific action

Once pressed the OK button, the Test Cases has been created and added to the list. At this point, it is possible to specify additional details for the test, for example: request parameters, headers, body content, tests to execute on the response.



### Duplicating a Test Case

Since a Test Case definition can be time consuming, a **Duplicate** button is provided too, in order to speed up the definition of new Test Cases, when these are similar with each other. When pressing this button, a dialog is prompted to the user, in order to specify the new name for the Test Case, as well as additional info.



### Changing a Test Case name

In case there is the need for changing the Test Case name, you can double click a row and then rename the Test Case name



### Bulk import of Test Cases

One of the best products for testing web services is PostMan.

Platform provides an **Import** button you can use to import a JSON file, expressed in PostMan format, representing the export of a Collection of Test Cases defined in PostMan. Thanks to this button, you can quickly migrate from a costly PostMan to Platform and reuse all your Test Cases. 

Supported Postman features are:

* Collection name
* Test case name
* HTTP method and URL
* request headers and query parameters
* body content
* one test script "after response", with a partial conversion of the Js Post API, for the most common scenarios



### Editing the Test Case

Once created a new Test Case, the main panel of the window can be used to define the Test Case details. These details are organized in 4 folders:

* **Parameters**
* **Headers**
* **Body**
* **Tests**

**Parameters** and **Headers** contain a free grid composed of parameter name and value: you can define any parameter. The value can includes variables, expressed as {{VARNAME}}. 

That means the request can send dynamic data, whose content can be defined at runtime, and inherits values coming form previous requests: you could define a login request, where the Tests folder is used to save a token and then pass forward the token value to the next request.

Special variables are {{DIGEST}} which gets back the current digest value for a mobile app and {{APP_VERSION}} which gets back the current application version for a mobile app.

**Body** can only be expressed for text content.

**Tests** can contain  javascript instructions, used for 2 purposes:

* testing expected values, like a response containing an attribute whose value is true
* saving the response content or part of it and reuse it in the next requests.

![](/assets/test-forldertests.png)


You can specify variables expressed as {{VARNAME}} both in request parameters, request headers and body content.
Predefined variables that do not require to be specified in Environment are:
COMPANY_ID, SITE_ID, APPLICATION_ID, APP_VERSION, USERNAME, DAY, DOW, MONTH, TODAY, NOW, UUID, RANDOM, RANDOM10, RANDOM100, RANDOM1000, COUNTER

Moreover, a top-bar is included, in order to quickly change the URL and a series of buttons:

* **Send** - when pressed, the request is executed and the Body folder is automatically shown, so that the response can be reported in the bottom area; a colored panel is also included in order to check out the outcome of the request: green for an OK request, red for NO OK.
* **Save** - when pressed, the main area is saved, i.e. URL and all 4 folders content
* **Environment** - this is a cross test case feature, used to define variables which can be referred through {{XXX}} variables in the folders described above. Platform is able to recognize special variable names and auto-set a value for them, when losing focus on the variable name. Recognized variables are: companyId, siteId, username, languageId, applicationId

![](/assets/test-env.png)



### How to execute a Test Case

As reported above, the **Send** button can be used to execute the Test Case.

When pressing it, the request is executed and when it ends, the response is reported on the bottom.

In case of a request successfully executed, a green box is shown on the top, otherwise, the same box is red colored.

![](/assets/test.outcom.png)

After the execution of each request, the corresponding Test script is automatically executed, if specified in the Tests folder: if it contains instructions like

**utils.addCustomApplUserPar\(name,value\)**

that value is stored in the current user session and can be referred in any subsequent request, through {{XX}} reference.



### How to create a Test Case from an action

Another way to create a Test Case is starting from a server-side action:

* click on the **Execute server-side action** button, on the bottom right part of the window
* click on the **Generate Test** button, which will ask for retrieving the input parameters/headers/body
* after confirming this dialog, another window is prompted.

![](/assets/test-gentestfromaction1.png)

The Generate Test window allows to specify the required information for creating a Test Case:

* a Test Case **name**
* a **Collection** the Test Case belongs to, through an editable combo-box
* which **kind of Test Case** will be created, among 3 alternatives

![](/assets/test-gentestfromaction3.png)











