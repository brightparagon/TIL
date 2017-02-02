#How to make subdocuments and query(populate) them in Mongoose?

###How to define in in Schema?
Let's say there are two models: Owner and Car. This is how to make subdocument schema in Mongoose below.
```javascript
const mongoose = require('mongoose');

const ownerSchema = new mongoose.Schema({
  name: String,
  age: Number,
  cars: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Car'
  }]
});
module.exports = mongoose.model('Owner', ownerSchema);

const carSchema = new mongoose.Schema({
  modelName: String,
  manufacturer: String,
  owner: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Owner'
  }
});
module.exports = mongoose.model('Car', carSchema);
```
Here is the schema relationship. One owner can have multiple cars and a car must have only one owner.
That's why **'cars'** property comes in ownerSchema as an array and **'owner'** property just as normal.

###How to populate them when doing CRUD?
#####Create
When saving an owner first, there's nothing to do additionally. It's the same as saving normal objects. Because at the monent when an onwer is saved, there's no car object attached to the parent(owner).

**create an owner**
```javascript
const mongoose = require('mongoose');
const Owner = mongoose.model('Owner');

module.exports.createOwner = function(req, res, next) {
  let owner = new Owner();
  owner.name = req.body.name;
  owner.age = req.body.age;
  owner.save(function(err, owner) {
    if(err) return next(err);
    res.json(owner);
  });
};
```
But when a car is saved newly, it has to be attached to its owner so that it could be populated when an owner is retrieved. Attaching a car to its owner would look like below.

**create a car**
```javascript
const mongoose = require('mongoose');
const Owner = mongoose.model('Owner');
const Car = mongoose.model('Car');

module.exports.createCar = function(req, res, next) {
  let car = new Car();
  car.modelName = req.body.modelName;
  car.manufacturer = req.body.manufacturer;
  // We need owner's ObjectId to relate it
  // I get it from session in this case
  car.owner = req.session.owner._id;
  car.save(function(err, car) {
    if(err) return next(err);
    res.json(car);
  });
  // Update an owner with a car newly saved.
  req.session.owner.cars.push(car);
  Owner.findByIdAndUpdate(req.session.owner._id, req.session.owner,
    {new: true}, function(err) {
    if(err) return next(err);
    // With {new: true} option it will return the updated data
  });
};
```
#####Retrieve
When getting an owner or a car, those need to be populated with the related property.

**get an owner**
```javascript
const mongoose = require('mongoose');
const Owner = mongoose.model('Owner');

module.exports.getOwner = function(req, res, next) {
  Owner.findById(req.query.ownerId).populate('cars').exec(function(err, owner) {
    if(err) return next(err);
    res.json(owner);
  });
};
```
**get a car**
```javascript
const mongoose = require('mongoose');
const Car = mongoose.model('Car');

module.exports.getCar = function(req, res, next) {
  Car.findById(req.query.carId).populate('owner').exec(function(err, car) {
    if(err) return next(err);
    res.json(car);
  });
};
```
#####Update and Delete
These can be done similarly as Create and Retrieve.

###Example with real data
**owner**

db.owners.find()
```javascript
{ "_id" : ObjectId("588855c9c2c1597d28aa045f"), "name" : "Bill", "age" : 27, "cars" : [ ObjectId("5888696220f5d99051321599"), ObjectId("588869c29a497c90cc434e40"), ObjectId("588869ca9a497c90cc434e41") ], "__v" : 0 }
```
**car**

db.cars.find()
```javascript
{ "_id" : ObjectId("5888696220f5d99051321599"), "owner" : ObjectId("588855c9c2c1597d28aa045f"), "modelName" : "E300", "manufacturer" : "BENZ", "__v" : 0 }
{ "_id" : ObjectId("588869c29a497c90cc434e40"), "owner" : ObjectId("588855c9c2c1597d28aa045f"), "modelName" : "M5", "manufacturer" : "BMW", "__v" : 0 }
{ "_id" : ObjectId("588869ca9a497c90cc434e41"), "owner" : ObjectId("588855c9c2c1597d28aa045f"), "modelName" : "A4", "manufacturer" : "AUDI", "__v" : 0 }
```
As shown above, the owner named Bill has three cars. 'cars' property(array) includes three ObjectIds which can be found respectively in cars collection. And those three cars has the same ObjectId which is Bill.

###Reference
http://stackoverflow.com/questions/15208711/mongoose-subdocuments-vs-nested-schema

http://mongoosejs.com/docs/populate.html

http://mongoosejs.com/docs/subdocs.html
