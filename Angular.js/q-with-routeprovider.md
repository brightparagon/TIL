#$q with routeProvider(ngRoute)
#####With ngRoute and $q we can make a reliable server-side router.

###In what point these two make that happen?
With ngRoute alone, it is only sure that entry paths are matched and linked to HTML files. In other words if there is something wrong with a server that needs to return data or other problems happen there, front pages won't be displayed correctly because data is not set.

We can avoid this kind of situation by using $q service with ngRoute. Because we can define how our application reacts to requests depending on the results from $q. If data returns successfully when a certain request arrives with a path this makes sure that data is fully set up before whole front things like HTML, CSS, Javascript are displayed.

###How to make it?
Here is a example code from my MEAN project.

```javascript
var app = angular.module('example.blog', ['ngRoute']);
app.config(['$routeProvider', function($routeProvider) {
	$routeProvider
    .when('/posts/list', {
			templateUrl: 'listPost.html',
      resolve: {
        posts: ["PostsLoader", function(PostsLoader) {
          return PostsLoader();
        }]
      },
			controller: 'listPostCtrl',
		})
		.otherwise({
			redirectTo: '/'
		});
}]);
```
When a request with '/posts/list' path comes, the 'resolve' property puts data which in this case is  'posts' into the designated controller which here is 'listPostCtrl'. The data is retrieved by the factory called 'PostsLoader'. And this code is below.

```javascript
app.factory('PostsLoader', ['Post', '$q', function(Post, $q) {
  // 'Post' is a factory made of $resource(ngResource)
  return function() {
    var delay = $q.defer();
    Post.query(function(posts) {
      delay.resolve(posts);
    }, function() {
      delay.reject('Unable to fetch posts');
    });
    return delay.promise;
  };
}]);

app.controller('listPostCtrl', ['$scope', 'posts', function($scope, posts) {
  $scope.posts = posts;
}]);
```
The parameter called 'posts' above in the controller is the data retrieved by $q in the factory. This way, we can make sure data is fully set before front things are rendered and react appropriately to errors when occurred.

###Reference
https://docs.angularjs.org/api/ngRoute/provider/$routeProvider

https://docs.angularjs.org/api/ng/service/$q

http://odetocode.com/blogs/scott/archive/2014/05/20/using-resolve-in-angularjs-routes.aspx

https://github.com/icyse/mean-blog/blob/master/public/javascripts/controllers/controllers.js
