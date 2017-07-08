# Passport
##### It's a node module that simplifies the process of handling authentication in Express.
###### It provides a way to work with several authentication 'strategies' like logging in with Google, Facebook, Twitter etc.

### Usage
To use this passport module in a web project, the first thing we need to do is to install the module and the strategy using npm.

**Install**
```javascript
npm install passport --save
npm install passport-local --save
```
In this case, the second command installs a module called passport-local, which means we use a local strategy, not other
strategies like Google or Facebook.

**Configure Passport**

To configure Passport module, we need to create a file called passport.js. Then we can use this module in a server app.

First, import passport, local strategy and mongoose.
```javascript
var passport = require('passport');
var LocalStrategy = require('passport-local').Strategy;
var mongoose = require('mongoose');
var User = mongoose.model('User'); // an example schema used to get a user object from MongoDB
```
The local strategy for Passport expects two pieces of data called username and password.
But, if you want to use a different property teamed with password instead of username,
you can configure that in an option object with a usernameField property in the strategy definition.

The example code would look like this.
```javascript
passport.use(new LocalStrategy({
    usernameField: 'email' // you can change this
  },
  function(username, password, done) {
    User.findOne({ email: username }, function (err, user) {
      if (err) { return done(err); }
      // Return if user not found in database
      if (!user) {
        return done(null, false, {
          message: 'User not found'
        });
      }
      // Return if password is wrong
      if (!user.validPassword(password)) {
        return done(null, false, {
          message: 'Password is wrong'
        });
      }
      // If credentials are correct, return the user object
      return done(null, user); // the first parameter is an error object
    });
  }
));
```
Now Passport needs to be added to the application that would require the Passport config and initialize Passport as middleware.

Import the module in the top of a server app just like other fundamental modules like express and bodyParser.
```javascript
var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var cookieParser = require('cookie-parser');
var bodyParser = require('body-parser');
var passport = require('passport');
```
And then require the passport configure file after importing modules above.
```javascript
require('./models/db'); // to access MongoDB -> User schema
require('./config/passport'); // make a folder structure your way
```
At last, Passport should be initialized as Express middleware just before the API routes are added.
```javascript
app.use(passport.initialize());
app.use('/api', routesApi);
```

### Reference
https://www.sitepoint.com/user-authentication-mean-stack/

https://www.npmjs.com/package/passport
