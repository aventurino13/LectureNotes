Weekend Challange 5 
===
OMDB API - Angular Routes
---

###Terminal  
```
  npm init     //creates package.json
  npm install --save angular bootstrap express body-parser angular-route mongoose
```
###index.html
```html
  <div ng-repeat="movie in 
```

###favorites.html
```html
  <h2> Favorites Page Here </h2>

```

###client.js
```javascript
  //creating angular module that will act as entire application
  var app = angular.module('movieApp', ['ngRoute']);
  
  //configuration (this config only contains routes)
  app.config(['$routeProvider', function($routeProvider) {
  $routeProvider
  .when('/search', {
  templateUrl:'views/search.html'
  controller: 'seachController',
  controllerAs:'vm'
  })
  .when('/favorites', {
  templateUrl:'views/favorites.html'
  controller: 'favoritesController',
  controllerAs:'vm'
  })
  .otherwise({
  template:'<h2> That is a 404! </h2>
  })
 }]);
  
```


###searchController.js
```javascript

  app.controller('seachController', ['seachService', 
  function(searchService){
  var self = this;                          //--> setting self so that 'this' refers to the wrong thing
  self.search = searchService.search;       //--> this connects the search funct view and controller to the service
  self.searchResult = searchService.searchResult; //--> this connects the search results obj view and controller to the service
  }]);
```

###favoritesController
```
  app.controller('favoritesController', ['favoritesServicefunction(){
    var self = this;
    self.favorites = favoritesService.favorites;
  }
```

###favoritesService
```javascript
  app.service('favoritesService', ['$http', function ($http) {
    var self = this;
    
    self.favorites = { list: [] };
    
    self.getFavorites = function (){
      $http({
        method: 'GET',
        url:'/favorites'
       }).then(function ( response ) {
        self.favorites.list = response.data;
       })
      };
        
     self.getFavorites();
     
     
     self.saveFavorites = function (movie) {
      $http({
        method: 'POST',
        url: '/favorites',
        data:
       }).then( function (response ) {
        console.log(response);
        self.getFavorites();
     })
     
```


###searchService.js
```javascript

  app.service('seachService', [$http, function ( $http ){
    var self = this;
  
    self.searchResult = { details: [] };  
  
    self.search = function(searchText) {
      $http({
        method: 'GET',
        url:'.....ombdurl' + searchText
      }).then( function ( response ){
        self.searchResult.details = response.data.Search;     //--> doing this way it keeps everything up to date
      });
    };
  }]);
```


###app.js
```
    var express = require('express');
    var app = express();
    var bodyParser = require('body-parser');
    var mongoose = require('mongoose');
    var path = require('path');
    var favorites = require('./routes/favorites.js');

    app.use(express.static( 'public' ));  //--> serves public folder 
    
    app.use(bodyParser.json());
    
    mongoose.connect('mongodb://localhost:27017/psi-movie-db');
    
    mongoose.connection.on('connected', function() {
     console.log('We connected to the db!');
    })
    
    mongoose.connection.on('err', function() {
     console.log('We did not connect to the db!');
    })
    
    app.use('/favorites', favorites);  //--> slash favorites on a get request with bring you to module
    
    app.listen( port, function () {
      console.log('listening on port:', port);
    }
```


###favorites.js (in routes)
```javascript
  var express = require ('express')
  var router = express.Router()
  var favorite = require('./models/favorites');
  
  --> SAME AS ABOVE --> var router = require('express').Router();
  
  router.get('/', function( req, res){     //--> you want only '/' because otherwise it would be '/favorites/favorites'
    Favorite.find({}, function(err, favorites){
      if(err) {
      console.log('error in favorites find:', err);
      res.sendStatus(500);
      } else {
        res.send(favorites);
      };
    });
  }
  
  router.post('/', function( req, res) {
    var newMovieObject = req.body;
    res.send('you hit the favorites POST');
    newMovie = new Favorite(newMovieObject);
    newMovie.save(function(err) {
      console.log('error:', error);
      res.sendStatus(500);
     } else {
      res.sendStatus(200);
  }
  
  module.exports = router;
  
```

###favorites.js (in modules)--> create schema
```javascript
  var mongoose = require('mongoose');
  var Schema = mongoose.Schema;
  
    var FavoriteSchema = new Schema ({
        --> define schema
       })
     
    var Favorite = mongoose.model('Favorite', favoriteSchema);
    
    modules.exports = Favorite;
        
```
