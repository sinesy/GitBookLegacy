# Example : how to get a value previously read from a SQL query

A SQL query can be executed through a Service Task. This task stores the result set read into a process property named "result" \(if not re-defined\).  
The value stored in that property is expressed in JSON format. Consequently, a specific value inside that JSON string can be fetched by converting the JSON string in a Javascript object and then access the object by referring attributes.

Javascript example related to the query:

```js
select CODE,VALUE from …
```

generating a JSON string:

```js
[{ "CODE": "...", "VALUE": "..." }]
```

```js
try {
  var result = execution.getVariable("result");
  var res = eval("(" + result + ")");
  if (res.length!=null &amp;&amp; res.length&gt;0) {
    for(var i=0; i&lt;res.length; i++) {
      execution.setVariable(res[i][CODE], res[i][VALUE]);
    }
  }
} catch(e) {}
```

Note: if you need to get the email address for the user initiating the process, this is the query to define:

```js
SELECT E_MAIL FROM SUB01_PEOPLE WHERE COMPANY_ID=:COMPANY_ID AND SUBJECT_ID IN (SELECT SUBJECT_ID_SUB02 FROM PRM01_USERS WHERE COMPANY_ID=:COMPANY_ID AND USER_CODE_ID=:INITIATOR) and E_MAIL is not null
```

---



