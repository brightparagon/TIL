#JSON Web Token
####It's an open standard that defines a self-contained way for transmitting information securely between parties as a JSON object.
#####Specifically, it is like this
* Generate a token(jwt) when a new user is registered or return a token when a registered user logged in
* This token is encrypted with a specific hashing algorithm like HMAC, sha256 and includes the user object(information)
* It is then checked by a middleware in Express(server) and decrypted & decoded into an usable json object
* This ojbect is going to be rendered in HTML files


###Usage
To use this module in a web project, we need to install this first. So run this on the command line.
```javascript
npm install jsonwebtoken --save
```
It is effective to make the jwt-generating method in the MongoDB schema. Because doing so, we can locate generating method in one easily accessable place.

This way we can call it whenever and wherever we need it like registering or signing in.

So import the module in a model schema js file like this.
```javascript
var jwt = require('jsonwebtoken');
```
Then the method would look like this below.
```javascript
userSchema.methods.generateJwt = function() {
  var expiry = new Date();
  expiry.setDate(expiry.getDate() + 7); // lasts a week

  return jwt.sign({
    _id: this._id, // ObjectId
    email: this.email, // object property
    name: this.name, 
    exp: parseInt(expiry.getTime() / 1000) // expiry
  }, "shhhhh"); // It is recommended to have a secret key as the environment variable in the server
};
```
We can add properties needed in the jwt.sign() function.

Now we need to utilize jwt in API end points to protect paths.
###Example
If we need to make a route for registering a new user, the register method in the server-side would look like this.
```javascript
var mongoose = require('mongoose');
var User = mongoose.model('User');

module.exports.register = function(req, res) {
  var user = new User();

  user.name = req.body.name;
  user.email = req.body.email;
  user.setPassword(req.body.password);

  user.save(function(err) {
    var token;
    token = user.generateJwt(); // generate the token here!
    res.status(200);
    res.json({
      "token" : token // this token includes information we need like an user object
    });
  });
};
```
At last, we need to protect API paths like only allowing certain people to access and see a page.
To do this, we need express-jwt module in the routing js file. So, install the module first.
```javascript
npm install express-jwt --save
```
Then use this as a middleware to protect the path you want.
```javascript
var jwt = require('express-jwt');
var auth = jwt({
  secret: 'shhhhh',
  userProperty: 'payload'
});

router.get('/api/pageToProtect', auth, ctrlOfpageToProtect);
```

###Reference
https://www.sitepoint.com/user-authentication-mean-stack/

https://www.npmjs.com/package/jsonwebtoken
