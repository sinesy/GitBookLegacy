# **Appendix B - a complete example with Google MD**

In blue methods provided by main\_page.jsp.

In orange the ones provided by Google Material Design library.

```js
<html>
    <head>

        <!-- Google Material Design libraries -->
        <link rel="stylesheet" href="./mdl/material.min.css">
        <script src="./mdl/material.min.js"></script>

        <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">

        <!-- <link rel="stylesheet" href="./mdl/datetimepicker/css/datepicker.css"> -->
        <link rel="stylesheet" href="./mdl/datetimepicker/material-datetime-picker.css">
        <link rel="stylesheet" href="./mdl/select/getmdl-select.min.css">

        <link href='https://fonts.googleapis.com/css?family=Roboto' rel='stylesheet' type='text/css'>

        <meta name="viewport" content="width=device-width, initial-scale=1.0">

        <link rel="stylesheet" href="./mdl/ext/styles/dialog-polyfill.css">
        <link rel="stylesheet" href="./mdl/ext/styles/material.indigo-pink.min.css">
        <link rel="stylesheet" href="./mdl/ext/lib/mdl-ext-eqjs.min.css">
        <link rel="stylesheet" href="./mdl/ext/styles/demo.css"> 

        <link rel="stylesheet" href="./mdl/pagination/pagination.css">

        <link rel="stylesheet" href="./scripts/utils.css">


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
            loadScript('../4ws/main_page.jsp?applicationId=TEST1',function() {
                // 2 after loading the infra js, execute login on Platform: that will load web pages variables (username, etc.) and initialize translations
                loadScript('./scripts/utils.js',function() {
                    try {
                        init(initCompleted);
                    }
                    catch(e) {
                          if (e.toString()=="Not authenticated") {
                            // show login dialog!
                            window.location="login3.html";
                        }
                        else {
                            alert(e);
                        }
                    }
                });

            });

            // 4. login completed: start app
            var startApp = function() {
            }


        </script>

    </head>
    <body>

        <script language="Javascript">


        function logoutFromApp() {
            try {
                new AsyncRequest().send(
                      "../logoutapp?applicationId=TEST1",
                      "GET",
                      null,
                      null,
                      function(jsonResponse) {
                      },
                      function() {}
                );
            } catch(e){}
            window.location = '../index.html';
        }


        function showMyList() {

              var abcStore = createComboStore(59);

              var countriesStore = createComboStore(49);

              var grid = createGrid({
                  panelId: 259,
                  functionId: “...”,
                  region: 'center',
                  listeners: {
                      rowclick: function(rowIndex,attributeName) {
                        var record = grid.store.list[rowIndex];
                        formPanel.store.baseParams.clientCode = record.clientCode;
                        formPanel.load();
                      }
                   }
              });

              var formPanel = createForm({
                title: "Cliente",
                region: 'south',
                height: 280,
                labelWidth: 150,
                autoLoadData: false,
                panelId: 269
              });

              var win = new AppWindow({
                title: "My List",
                items: [grid,formPanel]
              });
        }


        </script>

        <div class="demo-layout-transparent mdl-layout mdl-js-layout">
          <header class="mdl-layout__header mdl-layout__header--transparent" style="min-height: 40px" >
          <!-- 
            <div class="mdl-layout__header-row">
              <span class="mdl-layout-title">Track & Trace</span>
              <div class="mdl-layout-spacer"></div>
              <nav class="mdl-navigation">
              </nav>
            </div>
             -->
          </header>

          <div class="mdl-layout__drawer">
            <span class="mdl-layout-title">My Demo</span>
            <nav class="mdl-navigation">

                <a class="mdl-navigation__link" href="#" 
                    onClick="executeFunction('showMyList')" >MyList</a>
                <a class="mdl-navigation__link" href="#" 
                    onClick="window.location = 'logoutFromApp()" >Quit</a>

            </nav>
          </div>
          <main class="mdl-layout__content" id="mainContent" style="overflow-y: hidden;">
            <div class="page-content" style="text-align:center;width:100%; height:100%">
              <div class="mdl-spinner mdl-js-spinner" id="waitspinner"></div>
            </div>
          </main>

            <footer class="mdl-mini-footer" style="padding: 5" >
              <div class="mdl-mini-footer__left-section">
                <div class="mdl-logo">Dev</div>
                <ul class="mdl-mini-footer__link-list">
                  <li><a href="#">Me</a></li>
                </ul>
              </div>
            </footer>
        </div>

        <script language="Javascript">
          // vertically center the wait spinner...
          var y = document.body.clientHeight/2;
          var s = document.getElementById("waitspinner");
          s.style.top = y-s.clientHeight; //  is-active
        </script>

        <!-- date time picker -->
        <script src="./mdl/datetimepicker/polyfill.js"></script>
        <script src="./mdl/datetimepicker/moment.js"></script>
        <script src="./mdl/datetimepicker/it.js"></script>
        <script src="./mdl/datetimepicker/rome.standalone.js"></script>
        <script src="./mdl/datetimepicker/material-datetime-picker.js"></script>

        <!-- selector -->
        <script src="./mdl/select/getmdl-select.min.js"></script>

        <!-- Application functionalities -->
        <!--<script src="./scripts/xyz.js"></script>-->

        <script language="Javascript">


            // keep alive...
            var keepAliveThread = function() {
                setTimeout(function() {

                  new AsyncRequest().send(
                      contextPath+"/keepAlive?user="+username,
                      "GET",
                      null,
                      null,
                      function(jsonResponse) {
                        keepAliveThread();
                      },
                      function() {}
                  );

                },60000*5);
            };
            keepAliveThread();


            // listen for browser's window resizing...
            window.onresize = function(event) {
              resizeAllComponents();
            };

        </script>

        <!--<script src="https://maps.googleapis.com/maps/api/js?key=XXX" type="text/javascript"></script>-->

        <script src="./mdl/ext/scripts/dialog-polyfill.js" type="text/javascript" charset="utf-8"></script>
        <script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=default,es6"></script>
        <script src="./mdl/ext/scripts/eq.min.js" type="text/javascript" charset="utf-8"></script>
        <script src="https://code.getmdl.io/1.2.1/material.min.js" type="text/javascript" charset="utf-8"></script>
        <script src="./mdl/ext/lib/mdl-ext.min.js" type="text/javascript" charset="utf-8"></script>

    </body>
</html>
```

In case of unauthorized access because the user is not authenticated yet, the init method would fire an exception which leads to readirect to the login3.html page, where a login dialog is prompted, in order to authenticate into Platform.

index3.html

```js
<html>
<head>
<title>Demo</title>

<!-- Google Material Design libraries -->
<link rel="stylesheet" href="./mdl/material.min.css">
<script src="./mdl/material.min.js"></script>
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
<!-- <link rel="stylesheet" href="./mdl/datetimepicker/css/datepicker.css"> -->
<link rel="stylesheet" href="./mdl/datetimepicker/material-datetime-picker.css">
<link rel="stylesheet" href="./mdl/select/getmdl-select.min.css">

<link href='https://fonts.googleapis.com/css?family=Roboto' rel='stylesheet' type='text/css'>






<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>


.mdl-dialog {
  width: 400px;
  height: 270px;
}

.mdl-dialog-inv {
  width: 400px;
  height: 150px;
}

h4 {
  /* title color */
  color: rgb(4,30,65) !important;
}

h3 {
  /* title color */
  color: rgb(4,30,65) !important;
}

dialog {
  /* text color in dialogs */
  color: rgb(4,30,65) !important;
}

input {
  /* text color in dialogs */
  color: rgb(4,30,65) !important;
}

button {
  /* text color in buttons */
  background-color: rgb(0,154,191) !important;
  color: rgb(255,255,255) !important;
  font-family: 'eluxText' !important;
}

body {
  /* background color */
  background: rgb(4,30,65) !important;
}

.mdl-dialog__actions--full-width {
  /* all controls aligned on the left with 40px padding */
  padding: 0px 35px 8px 0px;
}

.mdl-dialog__content {
  /* title aligned on the left */
  padding: 20px 50px 24px
}

.mdl-textfield__label:after {
  background: rgb(4,30,65) !important;
}

</style>

</head>
<body>

<script>

  if (navigator.userAgent.indexOf("Mozilla")==-1) {
    alert("This web application is compatible with browsers Chrome and Mozilla Firefox!");
  }

</script>


<script>

function login() {
  var username = document.getElementById("username").value.toUpperCase();
  var password = document.getElementById("password").value;

  if (username!="" && password!="") {

          // show progress bar...
          var s = document.getElementById("waitspinner");
          s.style.top = 100;
          s.className += " is-active";

          //send the asynchronous request...
          new AsyncRequest().send(
              "../login?applicationId=TEST1&companyId=00000&siteId=100”+
             “&username="+username.toUpperCase()+
             "&password="+password+
             "&languageId=EN",
              "POST",
              null,
              null,
              function(jsonResponse) {
                var res = JSON.parse(jsonResponse);
                if (res.success==true) {
                      // valid login!
                      s.classList.remove("is-active");
                      window.location = "test3.jsp"
                }
              },
              function(status,response) { 
                s.classList.remove("is-active");

                //invalid credentials dialog
                var dialoginv = document.getElementById('invdialog');

                var showModalButton = document.querySelector('.show-modal');
                if (!invdialog.showModal) {
                  dialogPolyfill.registerDialog(dialoginv);
                }
                dialoginv.showModal();
              }
          );

  }
}



</script>

<div style="margin-top:5%">
<center>
<dialog class="mdl-dialog" id="logindialog">
   <div class="mdl-dialog__content" style="width:305px;height:40px;background:white">
     <h4>
      Demo  
       <div class="mdl-spinner mdl-js-spinner" id="waitspinner"></div>
     </h4>
   </div>
   <div class="mdl-dialog__actions mdl-dialog__actions--full-width" style="width:370px;height:170px;background:white">
       <form action="#"  autocomplete="off">

        <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
          <input class="mdl-textfield__input" type="text" id="username"  autocomplete="off">
          <label class="mdl-textfield__label" for="shipmentName">Username</label>
        </div>
        <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
          <input class="mdl-textfield__input" type="password" id="password"  autocomplete="off">
          <label class="mdl-textfield__label" for="shipmentPwd" >Password</label>
        </div>

            <div>
              <button type="button" class="mdl-button" onClick="login();">Login</button>
            </div>
        </form>
   </div>
</dialog>
</center>
</div>

<dialog class="mdl-dialog mdl-dialog-inv" style="display:none" id="invdialog">
       <div class="mdl-dialog__content">
         <p>
           Invalid credentials
         </p>
       </div>
     <form action="#">
       <div class="mdl-dialog__actions mdl-dialog__actions--full-width">
         <button type="button" class="mdl-button" onClick="window.location.reload();">Ok</button>
     </div>
    </form>
</dialog>


<script>

   // login dialog
   var dialog = document.getElementById('logindialog');
   var showModalButton = document.querySelector('.show-modal');
   if (! dialog.showModal) {
     dialogPolyfill.registerDialog(dialog);
   }
   dialog.showModal();

</script>



<script language="Javascript">
  // vertically center the wait spinner...
  var y = document.body.clientHeight/2;
  var s = document.getElementById("waitspinner");
  s.style.top = y-s.clientHeight; //  is-active
</script>

<!-- date time picker -->
<script src="https://unpkg.com/babel-polyfill@6.2.0/dist/polyfill.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.17.1/moment.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.17.1/locale/it.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/rome/2.1.22/rome.standalone.js"></script>
<script src="./mdl/datetimepicker/material-datetime-picker.js"></script>

<!-- selector -->
<script src="./mdl/select/getmdl-select.min.js"></script>

<script language="Javascript">

languageId = "EN";

</script>


<!-- Components infrastructure -->
<script src="./scripts/utils.js"></script>


</body>
</html>
```



