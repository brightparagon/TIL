#How to create a child model when a parent model is saved?
#####Quick Answer: make a custom function on schema, which allows us to access or control the model in another way.

###How to do this?
For example, we need to define our own function to save a child model automatically when a parent model is saved(I don't know if it is right to call these models a child or parent, anyway a child means a model referenced)
It would be like this below.
This is a child model(user model) that is going to be referenced by a parent model(post model here).
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
This is an uppper model(parent model, post model) that references a child(user).
```javascript
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var postSchema = new Schema({
  postedBy: { // this postedBy property can be considered as a child
    type: Schema.Types.ObjectId,
    required: true,
    ref: 'User'
  },
  title: {
    type: String,
    required: true
  },
  updated: {
    type: Date,
    default: Date.now
  },
  tags: [String]
});
postSchema.methods.createPostWithUser = function(data, callback){
  if (data.postedBy) { // save child model first(child is postedBy here)
    data.postedBy = User(data.postedBy);
    data.postedBy.save(function(err) {
      // if an error occurred save nothing by passing null
      callback(err, err ? null : Post(data));
    });
  } else { // proceed without dealing with user
    callback(null, Post(data));
  }
};
module.exports = mongoose.model('Post', postSchema);
```
Now we can use this custom function in a sever side when a request arrived from a client side like below.
```javascript
createPostWithUser({
  title: ...,
  ...,
  postedBy: req.params.userId // ObjectId of an user
}, function(err, doc) {
  if(err) do something for an error
  doc.save(); // finally save a post
});
```

###reference

http://stackoverflow.com/questions/14758761/mongoose-create-reference-on-model-save
