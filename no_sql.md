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
    - [[MongoDB Terminal]](#mongodb-terminal)
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
    - [Schema](#schema)
      - [Find by field](#find-by-field)
      - [Aggregate](#aggregate)

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

### [MongoDB Terminal]
use shelterDB // Create new db and/or use it
db.petCollection.insertOne({ pet: "dog", breed: 'chihuahua'}) // Creating a collection with a document
db.petCollection.find()

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
const documentId = new ObjectId("unique id string")
const documentTimestamp = documentId.getTimestamp() // YYYY-MM-DD HH:mm:ss
```

### [Connecting](#table-of-contents)

```javascript
const { MongoClient, ObjectId } = require("mongodb")
const seedData = require("./seed")

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
  .find({_id: new ObjectId("unique id string")})
  .toArray()
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

### [Update](#table-of-contents)

db.groceryColleciton.updateOne({item: "banana", {$set: { item: "apple"}}})
   Finds the docuemnt first document with item = "banana" and changes it to"apple"

The $set operator is used to update specific fields in the document. It's important to note that without $set, the update operation will replace the entire document.

`$set`
```javascript
const filter = { _id: new ObjectId('your_object_id_here') };
const update = { $set: { name: 'New Name', age: 31 } };

db.collection("collectionName").updateOne(filter, update);
  .then(results => console.log(results))
  .catch(err => console.error(err))
```

### [Delete](#table-of-contents)

```javascript
db.collection("collectionName").deleteOne({_id: new ObjectId("unique id string")})
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

### [Schema](#table-of-contents)

```javascript
const mongoose = require("mongoose")

const schema = new mongoose.Schema({
  email: {
    type: String,
    required: true,
    unique: true,
    alias: "username", // Alternate name for the property
    immutable: true // Property is read only
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
  partner: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User", // References the "User" model
    select: false, // Property isn't included in query by default
  }
})

module.exports = mongoose.model("Model Name", schema)
```

BSON Supports the data types String, Boolean, Number(Integer, Float, Long, Decimal128, ...), Array, null, Date, BinData


| Method                 | Description                                                       |
|------------------------|-------------------------------------------------------------------|
| .find()                | Find documents with the fields                                    |
| .findOne()             | Find the first document with the field                            |
| .findById(docIdString) | Find document by id string                                        |
| .aggregate()           | Advanced querying and aggregation operations                      |
| .count()               | Count the number of documents with the query                      |
| .distinct()            | Returns an array of distinct values for a specified field         |
| .limit(number)         | Limits the number of documents returned                           |
| .sort({field: "asc"})  | Sort in "ascending"/"asc"/1 order or "descending"/"desc"/-1 order |
| .skip(number)          | Skips a number of documents in a query                            |

#### [Find by field](#table-of-contents)

```javascript
.find({key: "value"})
```

#### [Aggregate](#table-of-contents)
