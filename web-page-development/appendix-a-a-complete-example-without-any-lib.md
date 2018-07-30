# Appendix A - a complete example without any lib

In blue methods provided by main\_page.jsp.

```js
<html>
    <head>
        <script language="Javascript">

            function loadScript(url, callback){

                // utility function always to include in any web page...
                var script = document.createElement("script")
                script.type = "text/javascript";

                if (script.readyState){  //IE
                    script.onreadystatechange = function(){
                        if (script.readyState == "loaded" ||
                                script.readyState == "complete"){
                            script.onreadystatechange = null;
                            callback();
                        }
                    };
                } else {  //Others
                    script.onload = function(){
                        callback();
                    };
                }

                script.src = url;
                document.getElementsByTagName("head")[0].appendChild(script);
            }

            // 3. callback invoked after the initialization
            var initCompleted = function() {
              startApp();
            }

            // 1. load dynamically the infra js...
            loadScript('../4ws/main_page.jsp?applicationId=XXX',function() {
                // 2 after loading the infra js, initialize user data... 
                // that will load web pages variables (username, etc.) and initialize translations
                try {
                    init(initCompleted);
                }
                catch(e) {
                    alert(e);
                }
            });

            // 4. login completed: start app
            var startApp = function() {

                // fill in the first combobox
                fillInCombo(49,"myCombo",true);

                // fill in the second combobox
                fillInCombo(59,"myCombo2",true);

                // fill in the form combobox
                combo = fillInCombo(49,"country",true);

                window.myComboChanged = function(combo) {
                    gridStore.load({
                      // here filtering conditions can be added, as well as startPos & blockSize...
                      filters: [{
                          attrName: 'country',
                          op: '=',
                          value: combo.value
                      }]
                    });
                }

                window.myCombo2Changed = function(combo) {
                    gridStore.load({
                      // here filtering conditions can be added, as well as startPos & blockSize...
                      filters: [{
                          attrName: 'abc',
                          op: '=',
                          value: combo.value
                      }]
                    });
                }


                // create a grid datastore
                var gridStore = new ListStore(
                    149,
                    function() {
                        // callback invoked after each data loading...
                        var numberFormatter2Dec = function(obj,decs,grouping) {
                            return numberFormatter(obj,2,false);
                        }
                        var list = gridStore.valueObjectList;
                        var myGrid = document.getElementById("myGrid");
                        while(myGrid.children.length>0)
                          myGrid.removeChild(myGrid.children[0]); // remove all previous rows...

                        for(var i=0;i<list.length;i++) {
                          list[i].country = combo.code2Desc(list[i].country);
                          myGrid.append( createTableRow(
                              list[i],
                              ["clientCode","name","createDate","totalAmount","abc","country"],
                              [null,null,dateTimeFormatter,numberFormatter2Dec,null,null],
                              [150,400,160,120,80,200]
                          ) );
                        }

                        // load also detail, with the first row in grid...
                        if (list.length>0)
                            formStore.load({
                                // filtering conditions needed to load a single record
                                filters: [{ attrName: "clientCode",value: list[0].clientCode }]
                            });

                    },
                    function() {
                        // callback invoked after each data loading with errors...
                        alert('Ops');
                    }
                );



                // create a form datastore
                var formStore = new FormStore(
                    159,
                    function() {
                        // callback invoked after each data loading...
                        var controlClientCode = document.getElementById("clientCode");
                        var controlName = document.getElementById("name");
                        var controlCreateDate = document.getElementById("createDate");
                        var controlTotalAmount = document.getElementById("totalAmount");
                        var controlAbc = document.getElementById("abc");
                        var controlCountry = document.getElementById("country");
                        controlClientCode.value = formStore.vo.clientId;
                        controlName.value = formStore.vo.name;
                        controlCreateDate.value = dateFormatter( formStore.vo.createDate );
                        controlTotalAmount.value = currencyFormatter( formStore.vo.totalAmount );
                        controlAbc.value = formStore.vo.abc;
                        controlCountry.value = formStore.vo.country;
                    },
                    function() {
                         // callback invoked after each data loading with errors...
                       alert('Ops');
                    }
                );

                gridStore.load({
                    // here filtering conditions can be added, as well as startPos & blockSize...
                });

            }

            // utility method
            function createTableRow(row,attributeNames,formatters,sizes) {
                var tr = document.createElement("tr");
                for(var i=0;i<attributeNames.length;i++) {
                  var td = document.createElement("td");
                  if (sizes!=null)
                    td.style="width:"+sizes[i];
                  tr.append(td);
                  var value = row[attributeNames[i]];
                  if (value==null)
                    value = "";
                  else if (formatters!=null && formatters[i]!=null) 
                      value = formatters[i](value);

                  var t = document.createTextNode( value );
                  td.append(t);
                }
                return tr;
            }

        </script>
    </head>
    <body>
        <select id="myCombo" onchange="myComboChanged(this);"></select>
        <br/>
        <select id="myCombo2" onchange="myCombo2Changed(this);"></select>
        <br/>
        <br/>
        <table id="myGrid" border=1></table>
        <br/>
        <table border=1 >
            <tr><td>Code</td><td><input type=text id="clientCode" style="width:200px" /></td></tr>
            <tr><td>Name</td><td><input type=text id="name" style="width:200px" /></td></tr>
            <tr><td>Date</td><td><input type=text id="createDate" style="width:200px" /></td></tr>
            <tr><td>Amount</td><td><input type=text id="totalAmount" style="width:200px" /></td></tr>
            <tr><td>ABC</td><td><input type=text id="abc"  /></td></tr>
            <tr><td>Country</td><td><select id="country" onchange=""></select></td></tr>
        </table>      
    </body>
</html>
```



