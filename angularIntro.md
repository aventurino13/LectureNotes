Angular Intro
===

NG Basics
---

  - Set up basic project - node, express, angular
  - Source files
  - Create "myApp" (ng app) and link to html
  - Create controller and link to div in html
  - Create ```var vm``` which will refer to our controller
  - Create and text ```ng-click``` to handle clikc events
  - Connect input fields via ```ng-model```
  - Create ```vm.ARRAYNAME``` which will hold our items
  - Push items from the input fields into the array when a button is clicked
  - Display items on DOM with ```ng-repeat```
  

Terminal Set-up
```
npm start
npm instal body-parser express --save  
```
  - Move anuglar.min.js into vendors folder
  
  index.html
  ```html
    <script src = "vendors/angular.min.js" charset="utf-8"></script>
    <script src = "scripts/ngBasics.js" charset="utf-8"></script>
    
    
    <body ng-app='myApp'>
      <h1>NG Basics</h1>
      <div ng-controller='InventoryController as ic'>
        <input type="text" placeholder="name" ng-model='ic.nameIn'/>
        <input type="text" placeholder="name" ng-model='ic.descriptionIn'/>
        <button ng-click='ic.addItem()'>Add Item</button>
      </div>
    </body>
  ```
  
  ngBasics.js
  ```javascript
    //app is the entire app
    var myApp = angular.module( 'myApp', [] );
    
    //controller is smaller part of the bigger app
    myApp.controller( 'InventoryController', function(){
      console.log('NG');
      //variable global to this controller
      var vm = this;
      //array attached to controller (makes it availbile to DOM)
      vm.items = [];
      //"vm" stands for "view model"
      vm.addItem = function(){
        console.log('in add item ng-click');
        var newItem = {
        name: vm.nameIn,
        description: vm.descriptionIn
        };
        
        vm.items.push( newItem ):
      }
      
    });//end inventory controller
     
  
  ```
  2-Way-Binder
    - vm.addItem in script = ic.addItem in html
  
  app.js
  ```javascript
    //requires
    //node modules
    var express = require ( 'express' );
    var app = express ();
    var bodyParser = require ( 'body-parser' );
    //our modules
    var index = require('.modules/index' );
    
    //uses
    app.use( express.static( 'public' ) );
    app.use( bodyParser.urlencoded( { extended: true } ) );
    //routes
    app.use('/', index );
    
    //globals
    var port = process.env.PORT || 3456;
    
    //spin up server
    app.listen( port , function () {
      
    })
  ```
  
  module ---> index.js
  ```
     var express = require ( 'express' );
     var router = express.Router();
     var path = require( 'path' );
     
     router.get('/', function( req, res ) {
      res.sendFile( path.resolve( 'public/views/index.html' );
     })
     
     module.exports = 
    
  ```
  
  
  
  
  
  
