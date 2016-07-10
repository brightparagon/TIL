#How is the collection name is set in MongoDB?

There are serveral naming conventions
* **lowercase** : MongoDB collection names are case-sensitive. Basically, when the schema is set the name of **it is determined in lowercase**.

* **plural** : While the name is set in lowercase, it is then **set in a plural form adding 's' to it**.

* **no word separators** : There are no word separators in MongoDB like 'user_name' or 'last_name'.

* **dot notation for higher detail collections** : It gives a way to see how collections are related.
For example, there are two collections names 'users' and 'pagevisits' each. 'users' is higher one and it populates 'pagevisits'.
Then, if you delete 'users' it also means a deletion of 'pagevisits' that belongs to 'users'.

### Example

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
  },
  hash: String,
  salt: String
});

module.exports = mongoose.model('User', userSchema);
```
When it it exported the default name of this user schema is going to be 'users'. 
So you can check this typing `db.users.find()` in MongoDB shell.

###Reference
http://stackoverflow.com/questions/9868323/is-there-a-convention-to-name-collection-in-mongodb
