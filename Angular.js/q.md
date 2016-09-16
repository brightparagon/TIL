###$q in AngularJS
#####It is the service which is quite similar to [promise in Javascript](https://github.com/brightlaw/TIL/blob/master/Javascript/promise.md) and can be considered as another version of promises/deferred object of [Kris Kowal's Q](https://github.com/kriskowal/q).

This service can be used in two ways.

The first one is like below.
It uses $q constructor.
```javascript
app.factory('PostLoader', ['Post', '$route', '$q', function(Post, $route, $q) {
  return function() {
    return $q(function(resolve, reject) {
      Post.get({postId: $route.current.params.postId}, function(error, post) {
        if(error) {
          reject('Unable to fetch post : ' + error.message);
        } else {
          resolve(post);
        }
      });
    });
  };
}]);
```

The another way to use it is like below.
It uses defer API.
```javascript
app.factory('PostLoader', ['Post', '$route', '$q', function(Post, $route, $q) {
  return function() {
    var delay = $q.defer();
    Post.get({postId: $route.current.params.postId}, function(post) {
      delay.resolve(post);
    }, function() { //this is a second function for dealing with an error
      delay.reject('Unable to fetch post '  + $route.current.params.postId);
    });
    return delay.promise;
    };
}]);
```

If our request toward a server is processed successfully then $q contains data we need.
And we can use that data somewhere we want by calling the function that returns a promise object
provided by $q.

For example, we can make the function as a factory or a service in AngularJS(It's done above though).
This $q service that assures a return value can be used very usefully with [Route Provider](http://odetocode.com/blogs/scott/archive/2014/05/20/using-resolve-in-angularjs-routes.aspx).
With Route Provider we can make sure all data we need in a certain page is fully loaded in a proper order before that page is loaded.

###Reference
https://docs.angularjs.org/api/ng/service/$q

http://programmingsummaries.tistory.com/345

http://haroldrv.com/2015/02/understanding-angularjs-q-service-and-promises/
