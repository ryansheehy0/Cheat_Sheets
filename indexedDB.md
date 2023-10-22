[Home](./README.md)

## [IndexedDB/idb](#table-of-contents)
IndexedDB is useful if you need to store large amounts of data on the client side that can quickly be retrieved.

IndexedDB is a NoSQL database that stores data in object stores in a binary format for efficiency. There is no inbuilt functionality for schemas.
- **Databases** store collections of object stores and data.
- **Object Stores** can hold multiple objects. Like containers in MongoDB.
- **Objects** are like objects in JS, but they are given a unique key to allow for easy retrieval. Like documents in MongoDB.
- **Key Paths/Primary Key** defines which one key in the objects, that are stored in an object store, should be used as the unique id. All objects in that object store need that primary key set to a unique value.
- **Indexes** are one key/property in the objects(in the object store) which allow for complex queries. Ex: In order to find all books of an author you can make an Author Index and do a getAll function.

IndexedDB allows for
- Automatic indexing
- Indexed CRUD operations are async
- Accessing data even when offline
- Structuring of data
- Allow for **transactions**
  - A sequence of CRUD operations where if one of them fails all the rest fail.
  - Ex: Moving money from account A to account B. If you cannot remove money from account A you don't want to add money to account B.

IDB is a library that makes it easier to work with indexedDB. Instead of callbacks it uses promises. `npm install idb`
- idb is cross browser compliant

## Table of Contents

<!-- TOC -->

- [IndexedDB/idb](#indexeddbidb)
- [Table of Contents](#table-of-contents)
- [Initializing DB](#initializing-db)
  - [IndexedDB initializing](#indexeddb-initializing)
  - [idb initializing](#idb-initializing)
- [CRUD Operations](#crud-operations)
  - [IndexedDB/idb Create/Add](#indexeddbidb-createadd)
  - [Read/Get](#readget)
    - [IndexedDB Read/Get](#indexeddb-readget)
    - [idb Read/Get](#idb-readget)
- [Creating Indexes](#creating-indexes)
  - [idb Get/Read with index](#idb-getread-with-index)

<!-- /TOC -->

## [Initializing DB](#table-of-contents)

### [IndexedDB initializing](#table-of-contents)

```javascript
// Get the indexedDB which will be different depending upon the platform.
const indexedDB =
  window.indexedDB ||
  window.mozIndexedDB ||
  window.webkitIndexedDB ||
  window.msIndexedDB ||
  window.shimIndexedDB

// Open the db
const dbName = "Library"
const version = 1 // Version of indexedDB
const request = indexedDB.open(dbName, version)

// Handle error
request.onerror = function(event){
  console.error("An error occurred with IndexedDB")
  console.error(event)
}

// When a new db is created or an existing db's version number has upgraded
  // This function allows you to specify the schema of the DB
request.onupgradeneeded = function(){
  const db = request.result
  // Define a new object store in the indexedDB
  const objectStoreName = "FictionalBooks"
  const primaryKey = "ISBN"
  const fictionalBooks = db.createObjectStore(objectStoreName, { keyPath: primaryKey }) // You can have the optional ,autoIncrement: true

  const indexName = "AuthorIndex"
  const keyName = "Author"
  fictionalBooks.createIndex(indexName, keyName)

  seed(db)
}
```

### [idb initializing](#table-of-contents)

```javascript
import {openDB} from "idb"
function initDB(){
  const dbName = "Library"
  const version = 1
  openDB(dbName, version, {
    upgrade: function(db){
      const objectStoreName = "FictionalBooks"
      // Make sure db doesn't already exist
      if(!db.objectStoreNames.contains(objectStoreName)){
        db.createObjectStore(objectStoreName, { keyPath: "ISBN"})
      }
      seed(db)
    }
  })
}
```

## [CRUD Operations](#table-of-contents)

### [IndexedDB/idb Create/Add](#table-of-contents)

```javascript
function seed(db){
  // Create the transaction
    const objectStores = "FictionalBooks" // String or an array of strings of all the object stores you want to access with the transaction
    const mode = "readwrite" // "readonly", "readwrite", or "versionchange". This is optional and the default value is readonly
  const transaction = db.transaction(objectStores, mode)

  // Choose which object store you are going to use with that transaction
    const objectStoreName = "FictionalBooks"
  const fictionalBooks = transaction.objectStore(objectStoreName)

  // Make data variable
  const data = [
    {
      ISBN: 9781234567, Title: "Book A", Author: "Author A", Genre: "Sci-Fi"
    },
    {
      ISBN: 9781234568, Title: "Book B", Author: "Author B", Genre: "Fantasy"
    },
    {
      ISBN: 9781234569, Title: "Book C", Author: "Author A", Genre: "Fantasy"
    },
  ]

  // Add the data with the object store in the transaction
  data.forEach(book => {
    fictionalBooks.add(book)
  })

  return transaction.complete
}
```

### [Read/Get](#table-of-contents)

To get an object from its primary key you use the `.get(primaryKey)` method.

To get more complex queries you have to use indexes.

#### [IndexedDB Read/Get](#table-of-contents)

```javascript
function get(){
  // Open the db
  const request = indexedDB.open("Library", 1)

  request.onsuccess = (event) => {
    const db = event.target.result
    // Make the transaction
    const transaction = db.transaction("FictionalBooks")
    const fictionalBooks = transaction.objectStore("FictionalBooks")

    const bookARequest = fictionalBooks.get(9781234567)

    bookARequest.onsuccess = (event) => {
      const bookA = event.target.result
      console.log(bookA)
    }

    bookARequest.oncomplete = () => {
      db.close()
    }
  }

  request.onerror = (event) => {
    console.error(`Error opening the database: ${event.target.error}` )
  }
}
```

#### [idb Read/Get](#table-of-contents)

```javascript
import {openDB} from "idb"
async function get(){
  const db = await openDB("Library", 1)
  try{
    const transaction = db.transaction("FictionalBooks")
    const fictionalBooks = transaction.objectStore("FictionalBooks")
    const bookA = await fictionalBooks.get(9781234567)
    console.log(bookA)
    const allBooks = await fictionalBooks.getAll()
  }catch(error){
    console.error(`An error occured with get: ${error}`)
  }finally{
    db.close()
  }
}
```

## [Creating Indexes](#table-of-contents)

```javascript
const indexName = "AuthorIndex"
const keys = "Author" // String or array of strings of the keys that are to be indexed
objectStore.createIndex(indexName, keys, { unique: false})
```

### [idb Get/Read with index](#table-of-contents)