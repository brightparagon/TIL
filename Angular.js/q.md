###$q in AngularJS
#####It is the service which is quite similar to [promise in Javascript](https://github.com/brightlaw/TIL/blob/master/Javascript/promise.md) and can be considered as another version of promises/deferred object of [Kris Kowal's Q](https://github.com/kriskowal/q).

This service can be used in two ways.

The first one is like below.
It is using $q constructor.
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
      };
    };
}]);
```

The another way to use it is like below.


