# How to move to other pages using $location with a parameter in it?
In many cases we use ng-href in a button or a tag with a parameter on the end of it like '#/posts/edit/post.id'
But sometimes we need to do something before moving to other pages. Then we make a button and add a function in javascript, attach it to the button. In that function some logics will be done and then the move needs to be done, in which case we use $location.

### So, how to put a parameter into $location?
It is pretty simple like below.
Let's suppose we already made a button and this is the function attached to it in the controller.

```javascript
app.controller('EditPostCtrl', ['$scope', '$location', function($scope, $location) {
  $scope.buttonToEdit = function(postId) { // postId is the database object id
    // do some logics here before moving to other pages
    $location.path('/posts/edit/' + postId);
  };
}]);
```
What we need to do is put the variable at the end of the url path. When executed a router will catch that path with a parameter and link the right page with data.

### Reference
https://docs.angularjs.org/api/ng/service/$location

http://stackoverflow.com/questions/22688779/passing-parameter-inside-location-path-in-angular
