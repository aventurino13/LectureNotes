# Angular Routing

_These notes originally from [antauth](https://github.com/antauth)_

In single page applications (SPAs), we often want to load new content without reloading the page.

Angular utilizes hash urls (e.g. http://localhost:3000/#/home.html) to allow us to handle our routes on the client. This works because browsers ignore everything after the #. With Angular routing, we can use what the browser ignores to show our users the content they requested.

## Using ngRoute

1. Include the source for angular-route in `index.html` under the source for angular.
```html
<script src="vendors/angular.min.js" charset="utf-8"></script>
<script src="vendors/angular-routes.min.js" charset="utf-8"></script>
```
2. Include the `ngRoute` module as a dependency for our angular app module.   
3. Use `ng-view` to mark the section of the `index.html` page where content will change based on route.
4. Define your routes  in a `config` function using `$routeProvider`.

## More detail/what's new

### ngRoute
An [Angular module](https://www.npmjs.com/package/angular-route) that we use to perform *client-side routing*.

```JS
var myApp = angular.module('myApp', ['ngRoute']);
```

### ng-view
Marks which section of the page should change when the route changes
ex: This is the area where we will swap view in and out - this is the only part that changes when you go to different pages

#### index.html
```HTML
<nav>  
  <ul>
  <li><a href="/#!/blue"></a></li>
  <li><a href="/yellow"></a></li>
  </ul>
</nav>
<ng-view></ng-view>
```

### $routeProvider
An angular service provided by `ngRoute` module, allows us to setup our client-side routes and their behavior.

**app.config** allows us to set configurations for our application, like our routes.

#### client.js
```JS
var myApp = angular.module('myApp', ['ngRoute']);

myApp.config(function($routeProvider) {         //--> MUST BE $routeProvider (similar to injecting)
  $routeProvider.when('/', {
    template: '<div> This is default</div>',
    controller: 'DefaultController as defCtrl'
  }).when('/blue', {
    templateUrl: 'views/pages/blue.html',
    controller: 'BlueController as blue'
  }).when('/yellow', {
    templateUrl: 'views/pages/yellow.html',
    controller: 'YellowController as YellowCtrl'
  }).otherwise('/');
});

myApp.controller('DefaultController', function () {
  console.log('default controller loaded');
  }
  
 myApp.controller('BlueController', function () {
  console.log('Blue controller loaded');
  }
  
   myApp.controller('YellowController', function () {
  console.log('Yellow controller loaded');
  }

```

#### /pages/blue.html
```
  <div>
    Blue page loaded
  </div>
```

#### /pages/yellow.html
```
  <div>
    yellow page loaded
  </div>
```

#### server.js
No server side routes that are the same as the client side routes
```JS
  app.get('/*', function (req, res){
    res.sendFile(path.join(_dirname,'public/views/index.html');
  }
  //THIS MUST BE THE LAST ROUTE IN SERVER --> /* is wildcard will respond to all requests
```

----
### $locationProvider
We use this service to allow us to use non-hash URLs.

#### client.js
```JS
var myApp = angular.module('myApp', ['ngRoute']);

myApp.config(function($routeProvider, $locationProvider) ) {         //--> MUST BE $routeProvider (similar to injecting)
  $routeProvider.when('/', {
    template: '<div> This is default</div>',
    controller: 'DefaultController as defCtrl'
  }).when('/blue', {
    templateUrl: 'views/pages/blue.html',
    controller: 'BlueController as blue'
  }).otherwise('/');
  
   $locationProvider.html5mode(true); 
});

myApp.controller('DefaultController', function () {
  console.log('default controller loaded');
  }
  
 myApp.controller('BlueController', function () {
  console.log('Blue controller loaded');
  }

```

#### index.html
```HTML
<head>
  ......all sources
  <base href="/">
</head>
<body>
  <nav>  
    <ul>
    <li><a href="/blue"></a></li>
    <li><a href="/yellow"></a></li>
    </ul>
  </nav>
  <ng-view></ng-view>
</body>
```
