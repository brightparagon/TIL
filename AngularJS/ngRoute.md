# ngRoute(routeProvider)
##### It's a module that provides routing services and directives for angular apps. And this is a great tool for making SPA(Single Page Application). This is similar to [UI-Router](https://angular-ui.github.io/ui-router/) and works similarly too.

### How to apply this into our apps?
First, we need to install this module using npm like below.
```javascript
npm install angular-route
```
And then include these into the index HTML.
```HTML
<script src="path/to/angular.js"></script>
<script src="path/to/angular-route.js"></script>
```
"path/to/" means a precise path to your dependencies folder.

Then load the module in our angular app which is maybe app.js.
```javascript
angular.module('example.app', ['ngRoute']);
```
Now we are ready to make a SPA with this module. We got two more things to do from now.

1. Routing Configuration that is going to be injected to app.js
2. The directive, <ng-view></ng-view>, which renders designated HTML files into itself -> SPA

This is an example code for Routing Configuration.
```javascript
var configs = angular.module('example.configs', ['ngRoute']);
configs.config(['$routeProvider', function($routeProvider) {
	$routeProvider
		.when('/', {
			templateUrl: 'main.html',
			controller: 'mainCtrl',
		})
    .when('/posts/upload', {
			templateUrl: 'uploadPost.html',
			controller: 'uploadPostCtrl',
		})
		.when('/signup', {
			templateUrl: 'signup.html',
			controller: 'signUpCtrl',
		})
		.when('/signin', {
			templateUrl: 'signin.html',
			controller: 'signInCtrl',
		})
		.otherwise({
			redirectTo: '/'
		});
}]);
```
This defines where each request with a path is matched to HTML and controller. Then inject this configuration module into the main app like below.

```javascript
var app = angular.module('example.blog', ['example.configs']);
app.controller('mainCtrl', ['$scope', function($scope) {
  // Do something here!
}]);
```

Finally, we need a directive for rendering.
```HTML
<html lang="en" ng-app="example.blog">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1">
  </head>

  <body>
    <h3><span>Example Blog</span></h3>

    <!-- ngRoute -->
    <ng-view></ng-view>

    <!-- javascript files -->
    <script src="lib/angular/angular.min.js"></script>
    <script src="lib/angular-route/angular-route.min.js"></script>
    <script src="js/configs/configs.js"></script>
    <script src="js/app.js"></script>
  </body>
</html>
```

### Reference
https://docs.angularjs.org/api/ngRoute

https://docs.angularjs.org/api/ngRoute/provider/$routeProvider

http://www.w3schools.com/angular/angular_routing.asp
