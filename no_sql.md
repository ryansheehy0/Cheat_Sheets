[Home](./README.md)

# No SQL
No SQL databases are typically used for unstructured or semi-structured data. They don't rely on a fixed schema, allowing it easier to make changes and scalability.

## Table of Contents

<!-- TOC -->

- [No SQL](#no-sql)
  - [Table of Contents](#table-of-contents)
  - [MongoDB](#mongodb)
    - [Connecting](#connecting)
    - [Schema](#schema)
    - [Create](#create)
    - [Get](#get)
      - [Find by field](#find-by-field)
      - [[]](#)
      - [Aggregate](#aggregate)
    - [Edit](#edit)
    - [Delete](#delete)

<!-- /TOC -->

## [MongoDB](#table-of-contents)
Data is stored in JSON like documents. A predefined schema for the db is optional. Data that is frequently accessed can be stored in the same document and thus allows for quicker reading of data unlike SQL where joins are necessary.

### [Connecting](#table-of-contents)
```javascript
const mongoose = require("mongoose")

const databaseUrl = "mongodb://localhost/subscribers" // usually a .env variable
mongoose.connect(databaseUrl, {useNewUrlParser: true})
const db = mongoose.connection
db.on("error", error => console.error(error))
db.once("open", () => console.log("Connected to db"))
```

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

MongoDb stores data as BSON(Binary JSON) instead of JSON. The problems that JSON has
- Limited number of basic data types like dates and binary data.
- JSON objects and properties don't have fixed lengths which makes it slower to retrieve data because you don't have fixed offsets(like in an array).

BSON Supports the data types String, Boolean, Number(Integer, Float, Long, Decimal128, ...), Array, null, Date, BinData


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
- Can you use a SQL like database in MongoDB
- How to do CRED operations outside of schema

### [Create](#table-of-contents)

```javascript
const Schema = require("../models/schema")

router.get("/", async (req, res) => {
  const schema = new Schema({
    email: "ryansheehy0@gmail.com",
    firstName: "ryan",
    lastName: "sheehy",
    age: 21,
  })
  try{
    const newSchema = await schema.save()
    res.status(201).json(data)
  }catch(error){
    res.status(400).json({error})
  }
})
```

### [Get](#table-of-contents)

```javascript
const Schema = require("../models/schema")

router.get("/", async (req, res) => {
  try{
    const data = Schema.find()
    res.json(data)
  }catch(error){
    res.send(500)
  }
})
```

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

#### []

#### [Aggregate](#table-of-contents)

```javascript

```


### [Edit](#table-of-contents)

```javascript
```

### [Delete](#table-of-contents)

```javascript
```