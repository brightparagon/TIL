#ngResource($resource)
#####It is an angular-based factory that makes a resource object that enables us to communicates with a server-side data [restfully](https://en.wikipedia.org/wiki/Representational_state_transfer).
In other words, we can retrieve all or a certain data, create, delete, update data object which is JSON here by using it.

**The basic form** is like this : ```$resource(url, [paramDefaults], [actions], options);```

###How to use it?
Firstly, we need to install it locally or globally(using -g option)

**Install**
```javascript
npm install angular-resource --save
```

Before we CRUD data, we need to define a factory or make a resource object directly.

**In the angular app**
```javascript
angular.module('example-app').factory('User', function($resource) {
  return $resource('/api/users/:email');
});
```
Here, '/api/users/:email' this url provides a full endpoint address.
And then we can use it in a controller.
```javascript
angular.module('example-app').controller('resourceController', function($scope, User) {
  
  // get an user
  var user = User.get({ email: $scope.email}, function(data) {
    console.log(data.email); // this data is actually an user
  });
  
  // get all users
  var users = User.query(function() {
    console.log(users);
  }
  
  // create a user(1) 
  $scope.user = new User();
  $scope.user.email = 'example@example.com';
  User.save($scope.user, function() {
    ...
  });
  
  // create a user(2)
  $scope.user = new User();
  $scope.user.$save(function() {
    ...
  });
});
```

**It is also possible to make a resource object directly**
```javascript
var User = $resource('/api/users/:email');

var newUser = new User($scope.user);

newUser.$save(function(data) { // data is an user object!
  console.log(data.name);
  console.log(data.email); 
  ...
});
```

Once $save is called this request from a client(angular app) goes to the server-side app.

If there is a middleware that functions as a router this request will go through it like below

**server-side app(express server)**
```javascript
// index.js contains routing codes
var routesApi = require('./routes/index');

// all url-requests that starts with '/api' will be catched by this middleware
app.use('/api', routesApi);
```

**index.js(it is also server-sided)**
```javascript
var express = require('express');
var router = express.Router();
var mongoose = require('mongoose');
var User = mongoose.model('User');

router.post('/signup', signUp);
router.get('/signin', signIn);
...

function signUp(req, res, next) {
  console.log('server - sign up');

  var user = new User(); // mongoose model
  user.name = req.body.name;
  user.email = req.body.email;
  ...

  user.save(function(error, user) {
    if(error) return next(error);
    res.status(200).json(user);
  });
};

module.exports = router;
```
