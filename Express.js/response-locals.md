# res.locals
##### It's an object that contains response local variables. Values stored in this res.locals could be reached in views only during request / response cycle.

### How useful?
It would be useful when it is necessary to maintain specific variables like session data(signed-in user) throughout the whole or some views.

### Example
```javascript
// express app
var express = require('express');
// router
var routes = require('./routes/index');
var app = express();
// middleware that loads data into res.locals before rendering views
app.use(function(req, res, next) {
  res.locals.signedUser = req.session.user;
  next();
});
// use router in the root level path
app.use('/', routes);
app.listen(process.env.PORT || 3000);
```
**It is important to put that middleware before the router, otherwise it can't be available in views.**

Then, we can use variables attached to res.locals in views like below.
```html
<!-- ejs -->
<div class="nav">
  <ul>
    <li><a href="/list">List</a></li>
    <% if(!signedUser) { %>
      <li><a href="/signup">Sign Up</a></li>
      <li><a href="/signin">Sign In</a></li>
    <% } %>
    <% if(signedUser) { %>
      <li><a href="/profile?userId=<%= signedUser._id %>"><%= signedUser.name %> is signed in!</a></li>
    <% } %>
    <% if(signedUser) { %>
      <li><a href="/signout">Sign Out</a></li>
    <% } %>
  </ul>
</div>
```

### Reference
http://egloos.zum.com/entireboy/v/4794353

http://expressjs.com/en/api.html

http://stackoverflow.com/questions/12550067/expressjs-3-0-how-to-pass-res-locals-to-a-jade-view
