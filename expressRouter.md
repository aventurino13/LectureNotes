Express Router
===
- Create routes in modules 
- Require the routes from modules in server files
- Allows you to update modules - makes it easier to handle larger projects. 

(1) Spin up new project
----
 - npm init
 - npm install body-parser express --save
 - Create files and folders

(2) Spin up Server
---
```javascript
  
  //requires
  var express = require ( 'express' );
  var app = express();
  var bodyParser = require ( 'body-parser');
  var path = require ( 'path');
  
  //globales
  var port = 3333;
  
  //uses
  app.use( experss.static ( 'public' ) );
  app.use( bodyParser.urlencoded( {extended: true} ) ):
  
  //spin up server
  app.listen ( port, function() {
    console.log ('server up on port-->', port);
  });
  
                      //test route
                      app.get( '/', funciton ( req, res ){
                        console.log( 'base url hit');
                      });
                       // --> MOVE THIS GET ROUTE INTO A NEW MODULE
  
```

(3)Create Modules Folder + Set-up index.js 
---
  - Require anything that will need to be used in modules
  - Export GET route
  

index.js
```javascript
  //index router for in class express routers lecture
  
  //requres
  var express = require ('express');
  var router = express.Router();
  
                    //MOVE GET ROUTE FROM SERVER
  router.get('/', function ( req, res ){
   console.log('base url hit in index.js');
  });
  
  //export module
  module.exports = router;
```
 
 (4) Require Module in Server
 
```javascript
  
  //requires
  var express = require ( 'express' );
  var app = express();
  var bodyParser = require ( 'body-parser');
  var path = require ( 'path');
  var index = require('./modules/index.js');
  
  //globales
  var port = 3333;
  
  //uses
  app.use( experss.static ( 'public' ) );
  app.use( bodyParser.urlencoded( {extended: true} ) ):
  //tell the server to use the router at 
  app.use('/', index);
  
  //spin up server
  app.listen ( port, function() {
    console.log ('server up on port-->', port);
  }); 
  
```
5) Create index.html


