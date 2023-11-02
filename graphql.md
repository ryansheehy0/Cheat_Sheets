[Home](./README.md)

# Graph QL
Graph QL allows the front end/client to retrieve the exact data it wants instead of specifying it on the server with a REST api.

Graph QL is a query language which the front end can use to only get back the data it needs instead of too much data or too little data.

## Table of Contents
<!-- TOC -->

- [Graph QL](#graph-ql)
  - [Table of Contents](#table-of-contents)
  - [Questions](#questions)
  - [Setting up the server](#setting-up-the-server)
  - [Schema on the server](#schema-on-the-server)
  - [Querying data on the client with Graph QL](#querying-data-on-the-client-with-graph-ql)
  - [Apollo Server](#apollo-server)
    - [Apollo with Express Server](#apollo-with-express-server)
    - [TypeDefs](#typedefs)
    - [Resolvers](#resolvers)
      - [Query Resolver](#query-resolver)
      - [Mutation Resolver](#mutation-resolver)

<!-- /TOC -->

## Questions
- types
- fields
- mutations
- interface
- type Comment implements Node? What does implements mean?
- enum
- union
- scalar
- If you can query from the client how do you prevent something like SQL Injections?
- What is the difference between the database schema and the graphQL schema?
- Authentication with Apollo Server?
- Self referencing Types?
- useQuery
- useMutation
- Apollo Cache

## Setting up the server

## Schema on the server

type School {
  _id: ID
  name: String
}

## [Querying data on the client with Graph QL](#table-of-contents)
Queries are described with a syntax that is like the returned JSON.

```javascript
// Query. getRockets is the name of the query
query getRockets {
  rocket {
    name
    thrust
    captain {
      name
      callSign
    }
  }
}

// Returned JSON
{
  "name": "Saturn V",
  "thrust": 7891000,
  "captain": {
    "name": "Neil Armstrong",
    "callSign": "Neil"
  }
}
```

You can also make your queries functions

```javascript
// Creates a query function what is required, The $id is the name of the arg
query getClass($id: ID!){
  class(id: $id){
    name
  }
}
```

## [Apollo Server](#table-of-contents)
Apollo Server runs on the server side. It
- Intercepts the incoming Graph QL
- Validates the query based on the schema
- Get the necessary data from the database
- Formats the data to the structure defined by the Graph QL
- Sends the formatted data back to the client

Graph QL uses a different schema than the underlying database. This allows for abstractions and security to prevent manipulation attacks on the database.

### [Apollo with Express Server](#table-of-contents)
In your server.js

```javascript
const express = require('express')
const { ApolloServer } = require('@apollo/server')
const { expressMiddleware } = require('@apollo/server/express4')

// Import the two parts of a GraphQL schema
const typeDefs = require("./schemas/typeDefs")
const resolvers = require("./schemas/resolvers")
// Create the apollo server
const server = new ApolloServer({typeDefs, resolvers})

const db = require('./config/connection')

const app = express()

// Create a new instance of an Apollo server with the GraphQL schema
const startApolloServer = async () => {
  await server.start()

  app.use(express.urlencoded({ extended: false }))
  app.use(express.json())

  // Provides a GUI to for Graph QL for your client
  app.use('/graphql', expressMiddleware(server))

  db.once('open', () => {
    app.listen(process.env.PORT/*Port for Heroku*/ || 3001, () => {
      console.log("Server is running")
    })
  })
}

startApolloServer()
```

### [TypeDefs](#table-of-contents)
Type Defs are string representation of the GraphQL Schema. They define the types, relationships between those types, and the operations that can be performed.

**Types** defines the shape of the data that can be queried.

In ./schemas/typeDefs.js

```javascript
const typeDefs = `
  type School {
    _id: ID # the id of the school
    name: String! # Every School requires a name
    location: String
    studentCount: Int
    # Add a queryable field to retrieve an array of Class objects
    classes: [Class] # The school has multiple classes
  }

  type Class {
    _id: ID
    name: String
    building: String
    creditHours: Int
    # Add a queryable field to retrieve a single Professor object
    professor: Professor
  }

  # Define what can be queried for each professor
  type Professor {
    _id: ID
    name: String
    officeHours: String
    officeLocation: String
    studentScore: Float
  }

  type Query {
    schools: [School]
    classes: [Class]
    professors: [Professor]
    class(id: ID!): Class # function which requires(because of the !) an id and returns the Class which matches that id
  }

  type Mutation {
    addSchool(name: String!, location: String!, studentCount: Int!): School
    deleteSchool(id: ID!) : School
  }
`

module.exports = typeDefs
```

### [Resolvers](#table-of-contents)
Resolvers tell Apollo Server how to link the Graph QL Schema with the data. That data can come from the backend database, 3rd party APIs, the server itself, etc.

There are 2 types of resolvers. Query and Mutations

All Query arguments:
- parent
- args
- context
- info

In Mongoose the `.populate` function is like a join function. it allows you to do a reference.
  - How does the .populate function work?

#### [Query Resolver](#table-of-contents)
The query resolver is used to get data.

```javascript
const { School, Class, Professor } = require('../models') // Import the database models

const resolvers = {
  Query: { // This is used to specify what each of the things in the type Query does
    schools: async () => {
      // returns the result from Mongoose
      return await School.find({}).populate('classes').populate({
        path: 'classes',
        populate: 'professor'
      });
    },
    classes: async () => {
      // Populate the professor subdocument when querying for classes
      return await Class.find({}).populate('professor');
    },
    professors: async () => {
      return await Professor.find({});
    },
    class: async (parent, args) => { // Resolving a query function
      // To get the args for that function use args
      return await Class.findById(args.id).populate("professor")
    }
  }
};

module.exports = resolvers;
```

#### [Mutation Resolver](#table-of-contents)
The mutation resolver is used to make any changes to the database. This includes adding data, deleting data, and updating data.

```javascript
  Mutation: {
    addSchool: async (parent, { name, location, studentCount }/* Deconstruct the args */) => {
      // Create and return the new School object
      return await School.create({ name, location, studentCount });
    },
  },
```