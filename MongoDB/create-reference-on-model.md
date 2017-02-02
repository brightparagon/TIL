#How to refer to other models in mongoose?

First we need to make a model that will be referred by another later.
###Example
**user.js**
```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var userSchema = new Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  }
});
module.exports = mongoose.model('User', userSchema);
```

Then create another model that is going to refer to User model
**post.js**
```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var postSchema = new Schema({
  //////////////////////////////// here!
  postedBy: {
    type: Schema.Types.ObjectId,
    required: true,
    ref: 'User'
  },
  ////////////////////////////////
  title: {
    type: String,
    required: true
  },
  isPrivate: {
    type: Boolean,
    required: true
  },
  content: {
    type: String,
    required: true
  },
  updated: {
    type: Date,
    default: Date.now
  },
  tags: [String]
});
module.exports = mongoose.model('Post', postSchema);
```
The type of postedBy property is 'Schema.Types.ObjectId'. There is no concept of strict relation(RDBMS) in MongoDB. So if we need to refer to other models from one, we have to user that ObjectId to refer to another model which is created by MongoDB automatically and it is of course unique.
And then there is 'ref' in postedBy. This means this postedBy property is going to refer to User model. So when saved in an actual database this postedBy data contains a certain User's ObjectId, which means this posting is created by a certain user.
