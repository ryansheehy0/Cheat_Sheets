[Home](./README.md)

# No SQL
No SQL databases are typically used for unstructured or semi-structured data. They don't rely on a fixed schema, allowing it easier to make changes and scalability.

There are 4 main types of no sql databases
- Document databases
- Key-Value stores
- Graph databases
- Column oriented databases

## Table of Contents

<!-- TOC -->

- [No SQL](#no-sql)
  - [Table of Contents](#table-of-contents)
  - [MongoDB](#mongodb)
    - [Installing](#installing)
    - [Starting and Stopping](#starting-and-stopping)
    - [MongoDB Shell](#mongodb-shell)
  - [Questions](#questions)
    - [Ids](#ids)
    - [Connecting](#connecting)
    - [Create](#create)
    - [Get](#get)
    - [Update](#update)
    - [Delete](#delete)
    - [Dollar Signs $](#dollar-signs-)
    - [Embedded Documents](#embedded-documents)
    - [Sort Skip Limit](#sort-skip-limit)
  - [Mongoose](#mongoose)
    - [Connecting](#connecting)
    - [Schema and Model](#schema-and-model)
    - [Mongoose CRUD](#mongoose-crud)
      - [Mongoose Create](#mongoose-create)
      - [Mongoose Read](#mongoose-read)
        - [Populate](#populate)
        - [Aggregate](#aggregate)
      - [Mongoose Update](#mongoose-update)
      - [Mongoose Delete](#mongoose-delete)
    - [Instance Methods/Virtuals](#instance-methodsvirtuals)
      - [Instance Methods](#instance-methods)
      - [Virtuals](#virtuals)
    - [Mongoose Embedded Documents](#mongoose-embedded-documents)

<!-- /TOC -->

## [MongoDB](#table-of-contents)
Data is stored in JSON like documents. A predefined schema for the db is optional. Data that is frequently accessed can be stored in the same document and thus allows for quicker reading of data unlike SQL where joins are necessary.

MongoDb stores data as BSON(Binary JSON) instead of JSON. The problems that JSON has
- Limited number of basic data types like dates and binary data.
- JSON objects and properties don't have fixed lengths which makes it slower to retrieve data because you don't have fixed offsets(like in an array).

MongoDb organizes things in these terms:

| Term              | Description                                                 |
|-------------------|-------------------------------------------------------------|
| Database          | These are separate databases                                |
| Collection        | These are like folders                                      |
| Documents         | Documents are BSON documents that usually hold related data |
| Embedded Document | An object in a document.                                    |

### [Installing](#table-of-contents)
- Install MongoDb [here](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition)
- Install Mongo Compass [here](https://www.mongodb.com/docs/compass/current/install/).

### [Starting and Stopping](#table-of-contents)
Start: `sudo service mongod start`

Verify it's started: `sudo service mongod status`

Stop: `sudo service mongod stop`

### [MongoDB Shell](#table-of-contents)

| Shell command                                                  | Description                                           |
|----------------------------------------------------------------|-------------------------------------------------------|
| mongo                                                          | Start the mongo shell                                 |
| show dbs                                                       | Show all dbs                                          |
| use dbName                                                     | Switch to dbName or create dbName if it doesn't exist |
| show collections                                               | Show all collections in the db                        |
| db.collection.insert({key: value, ...})                        | Insert a document                                     |
| db.collection.find({key: value})                               | Find documents                                        |
| db.collection.update({key: value}, { $set: { key: newValue }}) | Updates documents                                     |
| db.collection.remove({key: value})                             | Removes documents                                     |
| exit                                                           | Exists from shell                                     |

## Questions
- What does index({ name: 1}) mean?
  - Is this like the index in SQL databases?
- Sparse?
  - Property may not exist for every document
    - What are documents. When would you use this?
    - Can multiple documents be created with the same schema?
- select
  - If some property is select false how can you query it?
- What does the required function do?
- How can you change your schema in MongoDB

### [Ids](#table-of-contents)
Each document is automatically given a unique id called `_id`

The `ObjectId()` function ensures that the id is unique across the whole DB.

The id created by ObjectId has a timestamp associated with it.

```javascript
const documentId = new mongoose.Types.ObjectId("unique id string")
const documentTimestamp = documentId.getTimestamp() // YYYY-MM-DD HH:mm:ss
```

### [Connecting](#table-of-contents)

```javascript
const { MongoClient, ObjectId } = require("mongodb")
const seedData = require("./seed")

// Might be process.env.MONGODB_URI
const databaseUrl = "mongodb://localhost:27017" // Default local port of mongoDB. usually a .env variable
const client = new MongoClient(databaseUrl)
let db
const dbName = "dbName"

async function seedDBAndStartServer() {
  try {
    await client.connect()
    console.log("Connected to db");
    db = client.db(dbName);
    // If you don't have any seed data these can be skipped
    await db.collection('collectionName').deleteMany({});
    await db.collection('collectionName').insertMany(seedData);
    // Connect to express server
  } catch (err) {
    console.error('Mongo connection error: ', err.message);
  }
}
seedDBAndStartServer();
```

### [Create](#table-of-contents)

```javascript
db.collection("collectionName").insertOne( // Creates a document in the collection
  { key1: "value1", key2: "value2"}
)
  .then(results => console.log(results))
  .catch(err => console.error(err))

db.collection("petCollection").insertMany([ // Creates many documents in the collection
  { key1: "value1", key2: "value2"},
  { key1: "value1", key2: "value2"},
])
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

### [Get](#table-of-contents)

```javascript
db.collection("collectionName")
  .find({}) // Gets all documents int he collection
  .toArray()
  .then(results => console.log(results))
  .catch(err => console.error(err))

// You can use this to find by an id or you can use .findById
db.collection("collectionName")
  .find({_id: new mongooseObjectId("unique id string")})
  .toArray()
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

### [Update](#table-of-contents)

```javascript
const filter = { _id: new mongoose.Types.ObjectId('unique id string') } // Chooses which document
const update = { $set: { name: 'New Name', age: 31 } } // The $set allows you to update specific keys in the document without effecting the others.

db.collection("collectionName").updateOne(filter, update);
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

| Dollar Sign Operator | Description                                           |
|----------------------|-------------------------------------------------------|
| $inc                 | Increment the value by a certain amount               |
| $unset               | Remove the field from a document                      |
| $push                | Append element to an array field                      |
| $pull                | Removes all instances of a value from an array field  |
| $addToSet            | Adds an element to an array field if it doesn't exist |
| $pop                 | Removes the first or last element of an array field   |

### [Delete](#table-of-contents)

```javascript
db.collection("collectionName").deleteOne({_id: new mongoose.Types.ObjectId("unique id string")})
  .then(results => console.log(results))
  .catch(err => console.error(err))

// Delete the whole db collection
db.collection("collectionName").deleteMany({})
```

### [Dollar Signs $](#table-of-contents)

```javascript
db.collection("collectionName")
  .find({key: { $gte: 30 }}) // Gets all documents that have key greater than or equal to 30
  .toArray()
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

| Dollar Sign Operation | Description                                     |
|-----------------------|-------------------------------------------------|
| $gt                   | Greater than                                    |
| $gte                  | Greater than or equals                          |
| $lt                   | Less than                                       |
| $lte                  | Less than or equals                             |
| $ne                   | Not equals                                      |
| $in                   | Matches any of the values in an array           |
| $nin                  | Does not match any of the values in an array    |
| $exists               | Matches documents that have the specified key   |
| $type                 | Matches documents with a specific data type     |
| $regex                | Matches documents based on a regular expression |

### [Embedded Documents](#table-of-contents)
You can select based upon an object/embedded documents

```javascript
db.collection("collectionName")
  .find({"objName.key" : "value"})
  .toArray()
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

### [Sort Skip Limit](#table-of-contents)

| Method                | Description                                                       |
|-----------------------|-------------------------------------------------------------------|
| .limit(number)        | Limits the number of documents returned                           |
| .sort({field: "asc"}) | Sort in "ascending"/"asc"/1 order or "descending"/"desc"/-1 order |
| .skip(number)         | Skips just the first number of documents returned                 |

## [Mongoose](#table-of-contents)
MongoDb ORM to add additional features and make things easier.

Allows for schemas.

### [Connecting](#table-of-contents)

Don't need to import mongodb in your node package.

This is usually in your connection.js file.

```javascript
const mongoose = require('mongoose')

mongoose.connect('mongodb://127.0.0.1:27017/dbName')

module.exports = mongoose.connection
```

In your server.js file

```javascript
// Starts the db connection
const db = require("./connection")

// Import models
const { modelName } = require("./models/index")

db.once("open", () => {
  // Open express server
})
```

### [Schema and Model](#table-of-contents)
A schema defines how a document should laid out.

A model is a constructor function that is used to create, read, update, and delete documents based on that schema. Models apply the schema to the documents.

```javascript
const mongoose = require("mongoose")
const EmbeddedDoc = require("./embeddedDoc") // This is the exported model

const schema = new mongoose.Schema({
  email: {
    type: String,
    required: true,
    unique: true,
    alias: "username", // Alternate name for the property
    immutable: true, // Property is read only
    trimmed: true, // Trims leading and trailing whitespace
    maxLength: 280,
  },
  role: {
    type: String,
    enum: ["user", "admin", "editor"],
    required: function(){
      return this.role === "admin" // Required if the role is an admin
    },
  },
  firstName: String,
  lastName: String,
  fullName: {
    get: function(){
      return `${this.firstName} ${this.lastName}`
    },
    set: function(value){
      const parts = value.split(" ")
      this.firstName = parts[0]
      this.lastName = parts[1]
    }
  },
  age: {
    type: Number,
    default: 20,
    min: 18,
    max: 150,
    validate: {
      validator: function(value){
        return value >= 18
      },
      message: "Age must be at least 18."
    }
  },
  partner: { // Creating a reference to another Model
    type: mongoose.Schema.Types.ObjectId,
    ref: "User", // References the "User" model
    select: false, // Property isn't included in query by default
  },
  embeddedDoc: EmbeddedDoc.Schema, // This is creating an embedded document(object) which is different from a ref.
  createdAt: {
    type: Date,
    default: Date.now
  },
  id: {
    type: mongoose.Schema.Type.ObjectId,
    default: new mongoose.Types.ObjectId()
  }
},
{
  toJSON: {
    virtuals: true, // Allow for virtuals
  }
})

// Exports the model of the schema
module.exports = mongoose.model("Model Name", schema)
```

In your ./model/index.js you can group all of your schemas together

```javascript
const ModelName = require('./modelName');

module.exports = { ModelName };
```

BSON Supports the data types String, Boolean, Number(Integer, Float, Long, Decimal128, ...), Array, null, Date, BinData

### [Mongoose CRUD](#table-of-contents)
https://mongoosejs.com/docs/queries.html

#### [Mongoose Create](#table-of-contents)
Create a new document from a model

```javascript
const {ModelInstance} = require("./model/index")

// Creates and saves the doc
ModelInstance.create({
  email: "ryansheehy0@gmail.com",
  firstName: "ryan",
  lastName: "sheehy"
})
  .then(result => console.log('Created new document', result))
  .catch(err => handleError(err))

// You can also do it another way
const newDoc = new ModelInstance({
  email: "ryansheehy0@gmail.com",
  firstName: "ryan",
  lastName: "sheehy"
})
newDoc.save()

//  You have to manually save
const newDoc = await ModelInstance.insertMany({
  email: "ryansheehy0@gmail.com",
  firstName: "ryan",
  lastName: "sheehy"
})
newDoc.save()
```

#### [Mongoose Read](#table-of-contents)

```javascript
ModelInstance.find({}) // Finds all the documents that follow that schema
ModelInstance.find({key: "value"}) // Finds all documents that have the key that is equal to "value"
```

| Method                 | Description                                                       |
|------------------------|-------------------------------------------------------------------|
| .find()                | Find documents with the fields                                    |
| .findOne()             | Find the first document with the field                            |
| .findById(docIdString) | Find document by id string                                        |
| .findOneAndDelete()    | Deletes the document and returns the deleted doc.                 |
| .aggregate()           | Advanced querying and aggregation operations                      |
| .count()               | Count the number of documents with the query                      |
| .distinct()            | Returns an array of distinct values for a specified field         |
| .limit(number)         | Limits the number of documents returned                           |
| .sort({field: "asc"})  | Sort in "ascending"/"asc"/1 order or "descending"/"desc"/-1 order |
| .skip(number)          | Skips a number of documents in a query                            |
| .exec()                | Used to convert the other methods to return a promise             |
| .populate("key")       | key is a reference to a Model then it populates it.               |

```javascript
const mongoose = require("mongoose")

const query = Model.find({key: "value"})
const documents = await query.exec()

Model.findOneAndDelete({_id: mongoose.Types.ObjectId("unique id string")})
```

##### [Populate](#table-of-contents)
`.populate` is used to replace a specific field(which is a reference to another model) with the actual document from the referenced model.

```javascript
Book.findOne({title: "Book Title"})
  .populate("key", "model")
  .exec()
```

##### [Aggregate](#table-of-contents)
Group things together and then get statistics about that group.

The Aggregate pipeline describes the idea of a pipeline with stages. Each stage transforms the output and passes it to the next stage.

```javascript
const result = await Model.aggregate([
  // Documents where prices are less or equal to 5
  { $match: { price: { $lte: 5 } } }, // Used to filter which documents.
  {
    $group: { // Used to group documents together
      // Group by null (no additional grouping by id)
      _id: null, // How the documents are to be grouped
      //_id: "$key", // Groups all the documents based on the key. The keys have to be unique
      sum_price: { $sum: '$price' }, // The sum of the price fields in each of the docs
      avg_price: { $avg: '$price' },
      max_price: { $max: '$price' },
      min_price: { $min: '$price' },
    },
  },
])
```

Example:

```javascript
// Example data
{ "_id": 1, "name": "John Doe", "department": "Sales", "salary": 50000 }
{ "_id": 2, "name": "Jane Smith", "department": "Marketing", "salary": 60000 }
{ "_id": 3, "name": "Bob Johnson", "department": "Sales", "salary": 55000 }

// Aggregate
const pipeline = [{
    $group: {
      _id: "$department",
      totalEmployees: { $sum: 1 },
      averageSalary: { $avg: "$salary" }
    }
  }];

// Example group output
{ "_id": "Sales", "totalEmployees": 2, "averageSalary": 52500 }
{ "_id": "Marketing", "totalEmployees": 1, "averageSalary": 60000 }
```

#### [Mongoose Update](#table-of-contents)

```javascript
const filter = { name: "Ryan Sheehy"} // Get documents with name being Ryan Sheehy
const update = { age: 22 } // Updates the age in those documents to 22

Model.updateOne(filter, update) // Only returns success or failure
Model.findOneAndUpdate(filter, update, { new: true }) // Returns the updated document

Model.updateMany(filter, update)
```

#### [Mongoose Delete](#table-of-contents)

```javascript
Model.deleteMany(filter)

Model.deleteOne(filter)
Model.findOneAndDelete(filter, { new: true })
```

### [Instance Methods/Virtuals](#table-of-contents)

#### [Instance Methods](#table-of-contents)
Instance methods are methods that belong to the schema and are used to perform certain functions.

In your schema
```javascript
schema.methods.newCustomMethod = function(){
  console.log(`${this.firstName} ${this.lastName}`)
}
```

```javascript
const docName = new Model({
  email: "ryansheehy0@gmail.com",
  firstName: "ryan",
  lastName: "sheehy"
})

docName.newCustomMethod() // ryan sheehy

// There are also default methods
docName.get("key") // Gets the value fo the key
  // or
docName.get("key", String) // Gets the value fo the key as a string
```

#### [Virtuals](#table-of-contents)
Virtuals are like instance methods, but they are treated like any other value in the model. They aren't stored in the database, but are instead calculated when the virtual is called.

In your schema
```javascript
schema.virtual("newCustomVirtual").get(function(){
  return `${this.firstName} ${this.lastName}`
})
```

```javascript
const docName = new Model({
  email: "ryansheehy0@gmail.com",
  firstName: "ryan",
  lastName: "sheehy"
})

console.log(docName.newCustomVirtual) // ryan sheehy
```

### [Mongoose Embedded Documents](#table-of-contents)
Schema for nested objects.

```javascript
const mongoose = require('mongoose');

const managerSchema = new mongoose.Schema({
  name: { type: String, required: true },
  salary: Number,
});

const employeeSchema = new mongoose.Schema({
  name: { type: String, required: true },
  salary: Number,
});

const departmentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  manager: managerSchema, // Embedded document
  employees: [employeeSchema], // Embedded document
  lastAccessed: { type: Date, default: Date.now },
});

const Department = mongoose.model('Department', departmentSchema);

const managerData = { name: 'Taylor', salary: 80000 };
const employeeData = [
  { name: 'Ann', salary: 40000 },
  { name: 'Liu', salary: 50000 },
];

Department
  .create({ name: 'Shoes', manager: managerData, employees: employeeData })
  .then(data => console.log(data))
  .catch(err => console.error(err));

module.exports = Department;
```