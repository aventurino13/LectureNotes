Angular Services
===

### Services
Allows you to make controllers and write code onece and use it/make availbile wherever you need it.
1. Inject service in controller
* The things that are in service are not globally scoped - so it must be injected into angular app
```javascript
myApp.controller( 'InventoryController', function( $http, GetItems ) {.....}
```
2. Source in HTML file 
* my app must exist first before we can refer to it
```html
<script src="scripts/getItems-service.js" type="text/javascript"></script>
```
* You do not need to module.export beacuse you have already registered getItems as a part of my app
* Must inject getItems into myApp
* Try to make it so you have a little code in controller and alot of code in services
* If you have alot of things in functions then you have mobility to call those functions in many places
* Controller is communicator because what operations you want to perform and what you want to see on the DOM
* Using angular architecture to seperate things and get things connected



#### getItems-service.js
```javascript
  
  //getItems is name of service - registered getItems as part of myApp
  //must inject http to make it availible
  myApp.service( 'GetItems', function( $http ){
  
  this.getItems = function (){  //--> this refers to this whole services
  consle.log('in get Items');
  return http({    //--> you want return this whole http out of the function
    method: 'GET',
    url: '/inventory',
    })then( function success( response ) {
      console.log( 'resp:', response );
      return response.data;   //--> return throws the value out of the current function - makes it availible in service
  });// end success funciton
  
  
  
  })end servic function
```
* You do not need to module.export beacuse you have already registered getItems as a part of my app
* Must inject getItems into myApp
* Try to make it so you have a little code in controller and alot of code in services
* If you have alot of things in functions then you have mobility to call those functions in many places
* Controller is communicator because what operations you want to perform and what you want to see on the DOM
* Using angular architecture to seperate things and get things connected


#### my App
```javascript

  var myApp = angular.module( 'myApp', [] };
  
  myApp.controller( 'InventoryController', function($http, GetItems){
    console.log('-->NG');

    var vm = this;
    vm.items = [];
  
    vm.getItems = function(){     //--> you want to call this whenever you want to put it in a function
     GetItems.getItems.then(function(data){ //--> this is a function being called 
      console.log(' using dot then', data);
      vm.items = data;
      }
    }

    vm.addItem = function(){
      var newItem = {
        name: vm.nameIn,
        description: vm.descriptionIn
      };//end newItem
      $http({
        method:'POST',
        url: '/addItem',
        data: newItem,
      }).then(function success(response) {
       console.log('resp ->', response.data);
      //  getItems();
     });//end successs
     getItems();
    };//end addItem

  vm.nameIn = '';
  vm.descriptionIn = '';
  });//end inventory controller

```

The function was moved from angular app into a service -- now we can just call the function in the app instead of having the function below -->
```
  function getItems(){
    $http({
      method: 'GET',
      url:'/getItems',
    }).then(function success(response) {
     console.log('resp ->', response.data);
     vm.itemData = response.data;
    });
  }//end getItems
```

### ng-init
```
ng-init = ic.getItems();
```
* Runs on the initiation of this div
### .then()
```getItems().then(data)
```
* waits until thing it is called on is done
* you can pass in paramater -- that perameter will berepaced if the thing that then is called on returns something
* Ex: If get items returns a value it will replace data in the then

