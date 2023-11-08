[Home](./README.md)

# Graph QL
Graph QL allows the front end/client to retrieve the exact data it wants instead of specifying it on the server with a REST api.

Graph QL is a query language which the front end can use to only get back the data it needs instead of too much data or too little data.

## Table of Contents
<!-- TOC -->

- [Graph QL](#graph-ql)
  - [Table of Contents](#table-of-contents)
  - [Questions](#questions)
  - [File Structure](#file-structure)
  - [NPM](#npm)
  - [Querying and Mutating data with Graph QL](#querying-and-mutating-data-with-graph-ql)
  - [Useful Scripts](#useful-scripts)
  - [Server using Apollo Server](#server-using-apollo-server)
    - [Apollo with Express Server](#apollo-with-express-server)
    - [Authorization with JWTs](#authorization-with-jwts)
    - [TypeDefs](#typedefs)
    - [Resolvers](#resolvers)
      - [Query Resolver](#query-resolver)
      - [Mutation Resolver](#mutation-resolver)
  - [Client using Apollo](#client-using-apollo)
    - [Customizing Vite](#customizing-vite)
    - [Client Boilerplate with JWTs](#client-boilerplate-with-jwts)
    - [useQuery](#usequery)
    - [useMutation](#usemutation)
    - [Login Form Component Example](#login-form-component-example)

<!-- /TOC -->

## [Questions](#table-of-contents)
- interface
- type Comment implements Node? What does implements mean?
- scalar
- Authentication with Apollo Server?
  - JWTs

## [File Structure](#table-of-contents)

```
node_modules
client
  public
  src
    assets
    components
      ReactComponents.jsx
    pages
      ReactPages.jsx
    utils
      mutations.js
      queries.js
    App.jsx
    App.css
    main.jsx
  .gitignore
  index.html
  package.json
  vite.config.js
server
  models
    mongooseModels.js
  schemas
    resolvers.js
    typeDefs.js
  seeders
    seed.js
  package.json
  server.js
  connection.js
.gitignore
package.json
```

## [NPM](#table-of-contents)
- Client:
  - `npm install @apollo/client graphql`
- Server:
  - `npm install @apollo/server graphql`

## [Querying and Mutating data with Graph QL](#table-of-contents)
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

You can also run mutate functions

```javascript
mutate deleteClass($id: ID!){
  deleteClass(id: $id)
}
```

## [Useful Scripts](#table-of-contents)
These scripts can be put into your root's package.json

```javascript
    "start": "node server/server.js",
    "develop": "concurrently \"cd server && npm run watch\" \"cd client && npm run dev\"",
    "install": "cd server && npm i && cd ../client && npm i",
    "seed": "cd server && npm run seed",
    "build": "cd client && npm run build"
```

## [Server using Apollo Server](#table-of-contents)
Apollo Server runs on the server side. It
- Intercepts the incoming Graph QL
- Validates the query based on the schema
- Get the necessary data from the database
- Formats the data to the structure defined by the Graph QL
- Sends the formatted data back to the client

Graph QL uses a different schema than the underlying database. This allows for abstractions and security to prevent manipulation attacks on the database.

### [Apollo with Express Server](#table-of-contents)
In your server/server.js

```javascript
const express = require('express')
const { ApolloServer } = require('@apollo/server')
const { expressMiddleware } = require('@apollo/server/express4')
const path = require("path")
const { authMiddleware } = require("./utils/auth")

// Import the two parts of a GraphQL schema
const typeDefs = require("./schemas/typeDefs")
const resolvers = require("./schemas/resolvers")
// Create the apollo server
const server = new ApolloServer({typeDefs, resolvers})

const db = require('./config/connection')

const PORT = process.env.PORT || 3001
const app = express()

// Create a new instance of an Apollo server with the GraphQL schema
async function startApolloServer(){
  await server.start()

  app.use(express.urlencoded({ extended: true }))
  app.use(express.json())

  // If production server(with Heroku) then use the built react app which is in the dist folder
  if (process.env.NODE_ENV === 'production') {
    app.use(express.static(path.join(__dirname, '../client/dist')))

    app.get('*', (req, res) => { // Any routes are redirected to the index.html. This is because react is a Single Page Application and doesn't need different html files.
      res.sendFile(path.join(__dirname, '../client/dist/index.html'))
    })
  }

  // Provides a GUI to for Graph QL for your client
  // app.use('/graphql', expressMiddleware(server)) // Used without JWTs
  app.use('/graphql', expressMiddleware(server, {
    context: authMiddleware // Sets the context argument for GraphQL resolvers
  }))

  db.once('open', () => {
    app.listen(PORT, () => {
      console.log("Server is running")
    })
  })
}

startApolloServer()
```

### [Authorization with JWTs](#table-of-contents)
In ./utils/Auth

```javascript
const { GraphQLError } = require('graphql') // Used to make graphql errors
const jwt = require('jsonwebtoken')

const secretKey = 'This is you secret key for JWTs' // Should be in .env file
const expiration = '2h' // Expiration time for JWT

module.exports = {
  AuthenticationError: new GraphQLError('Could not authenticate user.', {
    extensions: {
      code: 'UNAUTHENTICATED',
    },
  }),
  authMiddleware: function({ req }){ // The apollo middleware function intercepts any requests. Not need to call next
    // The JWT token can be in one of these locations
    let token = req.body.token || req.query.token || req.headers.authorization
      // req.body.token allows the token to be sent in the GraphQL query
      // req.query.token allows the token to be sent in the url as /graphql?token=${token info}
      // req.headers.authorization allows the token to be sent in the authorization header

    // We split the token string into an array and return actual token
    if(req.headers.authorization){
      token = token.split(' ').pop().trim()
    }

    if(!token){
      return req
    }

    // if token can be verified, add the decoded user's data to the request so it can be accessed in the resolver
    try{
      const { data } = jwt.verify(token, secret, { maxAge: expiration });
      req.user = data
    }catch{
      console.log('Invalid token');
    }

    // return the request object so it can be passed to the resolver as `context`
    return req;
  },
  signToken: function (payload) { // Creates a new JWT
    return jwt.sign(payload, secretKey, { expiresIn: expiration });
  },
}
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

Resolver functions can have 4 arguments
- parent
  - the parent field of the current GraphQL Query
- args
  - These are the arguments for the typeDef functions
- context
  - This is mainly used by the client to send authentication information and other such information
- info
  - Provides info about the execution of the query


```javascript
// Example
query {
  user(id: "123") {
    name
    email
  }
}
// The parent is user
// The args object contains id. args.id
```

- context
  - Object shared among all resolvers in a particular GraphQL operation. This is mainly used for authentication details.
- info
  - Gives information about the current execution state of a query
  - Includes the field name, field AST(Abstract Syntax Tree), and more.

There are 2 main types of resolvers. Query and Mutations

#### [Query Resolver](#table-of-contents)
The query resolver is used to get data.

```javascript
const { School, Class, Professor } = require('../models') // Import the database models

const resolvers = {
  Query: { // This is used to specify what each of the things in the type Query does
    schools: async () => {
      // returns the result from Mongoose
      return await School.find({}).populate('classes'/*The classes field in School is populated with the classes model.*/).populate({
        path: 'classes', // specifies which model to use
        populate: 'professor' // the professor field in the classes model is populated with the professor model
      })
    },
    classes: async () => {
      // Populate the professor sub-document when querying for classes
      return await Class.find({}).populate('professor')
    },
    professors: async () => {
      return await Professor.find({})
    },
    class: async (parent, args) => { // Resolving a query function
      // To get the args for that function use args
      return await Class.findById(args.id).populate("professor")
    }
  }
}

module.exports = resolvers
```

#### [Mutation Resolver](#table-of-contents)
The mutation resolver is used to make any changes to the database. This includes adding, deleting, and updating data.

```javascript
const { School, Class, Professor } = require('../models') // Import the database models
const mongoose = require("mongoose")

const resolvers = {
  Mutation: {
    addSchool: async (parent, { name, location, studentCount }/* Deconstruct the args */) => {
      // Create and return the new School object
      return await School.create({ name, location, studentCount })
    },
    deleteSchool: async (parent, { id }) => {
      return await School.findOneAndDelete({_id: mongoose.Types.ObjectId(id)})
    }
  },
}

module.exports = resolvers
```


## [Client using Apollo](#table-of-contents)

### [Customizing Vite](#table-of-contents)
Add this to vite.config.js in `server: {}`

```javascript
    proxy: {
      '/graphql': {
        target: 'http://localhost:3001',
        changeOrigin: true,
        secure: false,
      },
    }
```

This allows the front end to make API calls to the running server which is on a different port.

### [Client Boilerplate with JWTs](#table-of-contents)
In App.jsx

```javascript
import { ApolloClient, InMemoryCache, ApolloProvider, /*For JWTs*/createHttpLink } from "@apollo/client"
import { setContext } from '@apollo/client/link/context' // For JWTs
  // The set context is a method to allow you to intercept graphQL queries and set the context(for the resolvers on the server)

// If you aren't using JWT
const client = new ApolloClient({
  uri: "/graphql", // Vite config which is the server
  cache: new InMemoryCache(), // Automatically caches queried data
})

// If you are using JWT
const httpLink = createHttpLink({
  uri: '/graphql',
})
const authLink = setContext((_, { headers }) => {
  const token = localStorage.getItem('id_token') // Get the JWT token stored in local storage
  return { // Changes the GraphQL query headers to include the JWT
    headers: {
      ...headers,
      authorization: token ? `Bearer ${token}` : '', // Bearer is convention for sending tokens over the authorization header
    },
  }
})
const client = new ApolloClient({
  link: authLink.concat(httpLink), // The link property tells Apollo Client where to send queries to. In this case it modies the headers and then sends it to /graphql
  cache: new InMemoryCache(),
})

export default function App() {
  return (
    <ApolloProvider client={client}> {/*Allows access to apollo hooks*/}
        <div></div>
    </ApolloProvider>
  )
}
```

In utils/auth.js

```javascript
import decode from 'jwt-decode';

class AuthService {
  getProfile() {
    return decode(this.getToken());
  }

  loggedIn() {
    // Checks if there is a saved token and it's still valid
    const token = this.getToken();
    return !!token && !this.isTokenExpired(token);
  }

  isTokenExpired(token) {
    try {
      const decoded = decode(token);
      if (decoded.exp < Date.now() / 1000) {
        return true;
      } else return false;
    } catch (err) {
      return false;
    }
  }

  getToken() {
    // Retrieves the user token from localStorage
    return localStorage.getItem('id_token');
  }

  login(idToken) {
    // Saves user token to localStorage
    localStorage.setItem('id_token', idToken);
    window.location.assign('/');
  }

  logout() {
    // Clear user token and profile data from localStorage
    localStorage.removeItem('id_token');
    // this will reload the page and reset the state of the application
    window.location.assign('/');
  }
}

export default new AuthService()
```

### [useQuery](#table-of-contents)
Allows react to make a Graph QL query to the server.

In utils/queries

```javascript
import { gql } from '@apollo/client'// Allows to parse queries as template literals

// Convention is to name queries as capital with underscores instead of spaces

// gql is a function which takes the template literal which is a graph QL query
export const QUERY_PROFILES = gql`
  query allProfiles {
    profiles {
      _id
      name
      skills
    }
  }
`

export const QUERY_SINGLE_PROFILE = gql`
  query singleProfile($profileId: ID!) {
    profile(profileId: $profileId) {
      _id
      name
      skills
    }
  }
`
```

In pages/Home.jsx

```javascript
import { useQuery } from '@apollo/client'

import ProfileList from '../components/ProfileList'
import ProfileForm from '../components/ProfileForm'

// Import the queries
import { QUERY_PROFILES, QUERY_SINGLE_PROFILE } from '../utils/queries'

export default function Home(){
  // loading and data are state, so when they change they tell react to re-render the page
  const { loading, data } = useQuery(QUERY_PROFILES)
  // data is data returned
  // loading is boolean for if the query has returned data or not

  // Putting arguments into queries
  const { loading: loadingSingle, data: dataSingle } = useQuery(QUERY_SINGLE_PROFILE, {
    variables: { profileId: profileId },
  })

  // When the data is loaded in(it acts like a state so it re-renders the page), this code is ran again and the profiles is set to the data?.profiles
  const profiles = data?.profiles || []

  return (
    <main>
      <div className="flex-row justify-center">
        <div
          className="col-12 col-md-10 mb-3 p-3"
          style={{ border: '1px dotted #1a1a1a' }}
        >
          <ProfileForm />
        </div>

        <div className="col-12 col-md-10 my-3">
          {loading ? (
            <div>Loading...</div>
          ) : (
            <ProfileList
              profiles={profiles}
              title="Here's the current roster of friends..."
            />
          )}
        </div>
      </div>
    </main>
  )
}
```

### [useMutation](#table-of-contents)
useMutation is used to allow React to send Graph QL mutations

In utils/mutations

```javascript
import { gql } from '@apollo/client';

export const ADD_PROFILE = gql`
  mutation addProfile($name: String!) {
    addProfile(name: $name) {
      _id
      name
      skills
    }
  }
`

export const ADD_SKILL = gql`
  mutation addSkill($profileId: ID!, $skill: String!) {
    addSkill(profileId: $profileId, skill: $skill) {
      _id
      name
      skills
    }
  }
`
```

In a component using mutations

```javascript
import { useState } from 'react';
import { useMutation } from '@apollo/client';

import { ADD_PROFILE } from '../../utils/mutations';

export default function Component(){
  const [name, setName] = useState('');

  // Sets the addProfile mutation method
  const [addProfile, { error }] = useMutation(ADD_PROFILE);

  // You can also remove cached mutations
  const [addProfile, { error }] = useMutation
    (ADD_PROFILE, {
      refetchQueries: [
        QUERY_PROFILES,
        'allProfiles'
      ]
    });


  const handleFormSubmit = async (event) => {
    event.preventDefault();

    try {
      // Uses the mutation function
      const { data } = await addProfile({
        variables: { name },
      });

      window.location.reload(); // Why? Wouldn't the state do it?
    } catch (err) {
      console.error(err);
    }
  };

  return (
    <div>
      <h3>Add yourself to the list...</h3>
      <form
        className="flex-row justify-center justify-space-between-md align-center"
        onSubmit={handleFormSubmit}
      >
        <div className="col-12 col-lg-9">
          <input
            placeholder="Add your profile name..."
            value={name}
            className="form-input w-100"
            onChange={(event) => setName(event.target.value)}
          />
        </div>

        <div className="col-12 col-lg-3">
          <button className="btn btn-info btn-block py-3" type="submit">
            Add Profile
          </button>
        </div>
        {error && (
          <div className="col-12 my-3 bg-danger text-white p-3">
            Something went wrong...
          </div>
        )}
      </form>
    </div>
  )
}
```

### [Login Form Component Example](#table-of-contents)

```javascript
import { useState } from 'react';
import { useMutation } from '@apollo/client';
import { Link } from 'react-router-dom';
import { LOGIN } from '../utils/mutations';
import Auth from '../utils/auth';

function Login(props) {
  const [formState, setFormState] = useState({ email: '', password: '' });
  const [login, { error }] = useMutation(LOGIN);

  const handleFormSubmit = async (event) => {
    event.preventDefault();
    try {
      const mutationResponse = await login({
        variables: { email: formState.email, password: formState.password },
      });
      const token = mutationResponse.data.login.token;
      Auth.login(token);
    } catch (e) {
      console.log('error', e);
    }
  };

  const handleChange = (event) => {
    const { name, value } = event.target;
    setFormState({
      ...formState,
      [name]: value,
    });
  };

  return (
    <div className="container my-1">
      <Link to="/signup">← Go to Signup</Link>

      <h2>Login</h2>
      <form onSubmit={handleFormSubmit}>
        <div className="flex-row space-between my-2">
          <label htmlFor="email">Email address:</label>
          <input
            placeholder="youremail@test.com"
            name="email"
            type="email"
            id="email"
            onChange={handleChange}
          />
        </div>
        <div className="flex-row space-between my-2">
          <label htmlFor="pwd">Password:</label>
          <input
            placeholder="******"
            name="password"
            type="password"
            id="pwd"
            onChange={handleChange}
          />
        </div>
        {error ? (
          <div>
            <p className="error-text">The provided credentials are incorrect</p>
          </div>
        ) : null}
        <div className="flex-row flex-end">
          <button type="submit">Submit</button>
        </div>
      </form>
    </div>
  );
}

export default Login;
```