Angular Services
===
* Allows you to make controllers availbile whereever you need it

#### getItems-service.js
```javascript
  
  //getItems is name of service
  myApp.service('getItems', function (){
  
  this.getItems = function (){  //--> this refers to this whole services
  consle.log('in get Items');
  http({
    method: 'GET',
    url: '/inventory',
    })then( function success( response ) {
      console.log( 'resp:', response );
      return response.data;   //--> return throws the value out of the current function - makes it availible in service
  }
  
  
  })
```
