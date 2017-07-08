# ./bin/www
##### It's a file containing setup codes & scripts like port number, making & testing server, etc.

### Example
This looks like below.
```javascript
var app = require('../app');
var http = require('http');

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

var server = http.createServer(app);

server.listen(port);
...
```

### What is it for?
Making this file outside the main project file makes it possible to set aside specific server codes from app.js file.
So that app.js file could only have logical codes, not environmental setting codes. It allows to manage the application with various situations like running the app on a different port, testing the app and restarting the app, etc.

We can make our own scripts and this is the example in package.json below.
```json
{
  "name": "MEAN-blog",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  }
}
```

### Reference
http://stackoverflow.com/questions/23169941/what-does-bin-www-do-in-express-4-x

http://stackoverflow.com/questions/36638123/learning-node-js-express-js-whats-the-deal-with-bin-www
