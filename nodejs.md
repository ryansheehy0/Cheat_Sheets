
[Home](./README.md)

# NodeJS
NodeJS is used to run JavaScript outside of the browser.

Somethings work differently when using JS in NodeJS then in the browser. This cheat sheet will cover those differences.

## Table Of Contents
- [Getting Started](#getting-started)
- [Node Package Manager(NPM)](#node-package-managernpm)
  - [Scripts](#scripts)
  - [Importing](#importing)
  - [Exporting](#exporting)
- [Miscellaneous](#miscellaneous)
- [Things that don't work](#things-that-dont-work)
- [this keyword](#this-keyword)
- [Global Variables](#global-variables)
  - [Process](#process)
    - [Arguments from the Terminal](#arguments-from-the-terminal)
- [Events](#events)
  - [Emitting Events](#emitting-events)
  - [Receiving Events](#receiving-events)
- [File System](#file-system)
  - [Reading to Files](#reading-to-files)
  - [Writing to Files](#writing-to-files)
  - [Appending to Files](#appending-to-files)
- [Path](#path)
- [Node-fetch](#node-fetch)
- [Packages](#packages)
  - [inquirer](#inquirer)
  - [express](#express)
    - [Express HTTP Methods](#express-http-methods)
    - [Parameters](#parameters)
    - [Routers](#routers)
    - [Middleware Functions](#middleware-functions)
    - [View Engines](#view-engines)
      - [EJS](#ejs)
    - [Front end and Back end](#front-end-and-back-end)
  - [jest](#jest)
  - [mysql2](#mysql2)
    - [mysql2 with Promises](#mysql2-with-promises)
    - [Prevent SQL Injections](#prevent-sql-injections)
  - [dotenv](#dotenv)
  - [bcrypt](#bcrypt)
    - [Creating a Hash](#creating-a-hash)
    - [Comparing a Password](#comparing-a-password)

## Getting Started
Run `node -v` to see what version of node you have. If you don't have node you can install it from [here](https://nodejs.org/en).

You can run `node script.js` or `node script` to run a JS file.

## Node Package Manager(NPM)
NPM is used to install dependencies/packages for NodeJS code.

|                           |                                                                                                             |
|---------------------------|-------------------------------------------------------------------------------------------------------------|
| `npm init`                | Sets up a package.json file in order to keep track of needed dependencies.                                  |
| `npm init -y`             | Sets up a package.json file with the default settings.                                                      |
| `npm install <package>`   | Installs the package for your project. Puts it in your package.json                                         |
| `npm install <package>@8.2.4`   | Installs the package with the version 8.2.4 for your project. Puts it in your package.json            |
| `npm i --save-dev <package>` | Installs the package as a dev package.                                                                   |
| `npm uninstall <package>` | Uninstalls the package for your project.                                                                    |
| `npm install`             | Installs all the dependencies if there is a package.json file and if the packages aren't already installed. |

package-lock.json locks the versions of the packages so that new version don't brake your code.

- devDependencies are dependencies that are only applied when developing and not in the production release of the app.

### Scripts
Inside the package.json

```javascript
"scripts": {
  "start": "node index.js",
  "test": "jest"
}
```

Running a script
`npm run scriptName`

### Importing
To import the exported variable you can do `const module = require("./filepath.js")`

In order to import from a package you do `const package = require("packageName")`

You can import json directly `const json = require("./file.json")`

### Exporting
To export you use the module.exports object

```javascript
module.exports = {
    function1: aFunctionThatDoesSomething,
    variable1: "test",
}
```

## Miscellaneous
- Functions that end in "sync" are blocking functions which means they force the other code to wait until it it done.
- index.js is the default location for node.
    - If you run `node ./` it will look for index.js first.

## Things that don't work
- window global variable
- alert, prompt, and confirm

## this keyword
- In order to use the this keyword you have to be inside a function.

## Global Variables

|           |                                                                                       |
|-----------|---------------------------------------------------------------------------------------|
| global    | Global for all files in your program. Like the window global variable in the browser. |
| process   | Info and controls over the current node environment.                                  |
| console   | Log info to the console.                                                              |
| module    |                                                                                       |
| Buffer    | Used to handle binary data.                                                           |
| __dirname | Specifies the absolute path of the currently running JS file.                         |

### Process
`process.platform` get what platform the node is running on like linux.

`process.env.NAME` get the environment variable called NAME

`server.address().port` gets the current port the server is running on.

#### Arguments from the Terminal
process.argv is an array that contains the command-line arguments.

```
Terminal: node ./ "This is a test" arg1
index.js: console.log(process.argv)
Console:
[
  '/path/to/node/executable',
  '/path/to/your/javascript/file.js',
  'This is a test',
  arg1
]
```

## Events

### Emitting Events
```javascript
const { EventEmitter } = require('events')
const eventEmitter = new EventEmitter

eventEmitter.emit("eventName")
```

### Receiving Events
```javascript
eventEmitter.on("eventName", () => {
})
```

## File System
`const fs = require('fs')` or with premisses `const fs = require('fs').promises`

### Reading to Files

```javascript
const encodingType = "utf8"

// Blocking/Sync
const file = fs.readFileSync("filepath.txt", encodingType)

// Non-Blocking
fs.readFile("filepath.txt", encodingType, (error, file) => {/* function when file is loaded*/})

// Asynchronous/Promises
async function loadFile() {
    const file = await fs.readFile("filepath.txt", encodingType)
}
```

### Writing to Files

```javascript
fs.writeFile("./filepath.txt", "Written data", error => {error ? console.log(error) : false})
```

### Appending to Files

```javascript
fs.appendFile("./filepath.txt", "Written data", error => {error ? console.log(error) : false})
```

## Path
Used to make working with file paths easier.

`const path = require("path")`

## Node-fetch
Allows you to use the fetch function in node

`const fetch = require('node-fetch')`

## Packages

| Package  | Description                                            |
|----------|--------------------------------------------------------|
| inquirer | Used to simply get user input from the terminal        |
| express  | Simplifies HTTP-related tasks usually for making APIs. |
| jest     | Used for tests inside node.                            |
| mysql2   | MySQL library.                                         |
| dotenv   | Used for working with environment variables.           |
| bcrypt   | Used to create hashes for passwords.                   |

### inquirer
Used to simply get user input from the terminal.

Use  `npm install inquirer@8.2.4` to use require with inquirer.

```javascript
const inquirer = require('inquirer')

async function askQuestion(question, answerName, validationFunction){
  // List can be an array of strings or an array of objects with name and value
  let list = [`option 1`, `option 2`, `option 3`]
  list = [
    {name: `option 1`, value: 1},
    {name: `option 2`, value: 2},
    {name: `option 3`, value: 3},
  ]
    // name is what's displayed to the user
    // value is the value that is returned if the user chooses that option
  return new Promise((resolve, reject) => {
    inquirer.prompt([
      {
        type: 'input',
        name: answerName,
        message: question,
        validate: validationFunction,
        choices: type === `list` ? list : undefined,
      }
    ])
    .then(answer => {resolve(answer)})
    .catch(error => {reject(error)})
  })
}
```

The validation function should return true if the input is valid or return an error message.

```javascript
function validationFunction(input){
  if(input === "Test"){
    return true
  }
  return `The input must be "Test"`
}
```

### express
Simplifies HTTP-related tasks usually for making APIs. It's a framework for handling http requests.

```javascript
// server.js
const express = require("express")
const path = require("path")

const app = express()

// Settings
const settingName = "view engine"
const settingValue = "ejs"
app.set(settingName, settingValue)

// Middleware. Middleware functions are functions that can intercept and process incoming requests before they reach route handlers.
  // You need to parse the data because it comes in as a stream of binary data in packets that need to be constructed together
  // The content type header defines which middleware is triggered.

app.use(express.json()) // Parses the json body to an object
app.use(express.static('public')) // Setting for serving static files from the public folder. You can directly call the file. Ex: localhost:3000/images/image.jpg
app.use(express.urlencoded({ extended: true })) // Old browsers might send json through URL encoded

// HTTP Methods/Endpoints

// Listen
const port = process.env.PORT || 3000 // This is used when deploying on 3rd party servers. The port already defined or port 3000
app.listen(port, () => {
  // Optional function that is run when connected to the port
  console.log(`Server is running on ${port}.`)
})
```

- Always start your listening after you have defined all of your routes so the server can start with routes already defined.

#### Express HTTP Methods
Making/Receiving an http method uses the format of `app.httpMethod("path", callbackFunction)`
- The path is what is after the URL. By default the path is "/".
  - Ex: https://www.rscheatsheets.com/
  - You can also make the path "*" which will catch all other terms
    - This has to be placed after other http methods or else the "*" will overwrite the other http methods.
- The callbackFunction can take the arguments of request, response, and/or nextFunction

```javascript
app.get("/", (req, res) => {
  // Gets data from the server
  console.log("Test") // Outputs to the terminal of the server
})
app.post("/", (req, res) => {
  // Creates new data in the server
  // Used for login in
  const data = req.body
})
app.put("/", (req, res) => {
  // Replaces a resource in the server
})
app.delete("/", (req, res) => {
  // Removes data in the server
})

app.patch("/", (req, res) => {
  // Changes some of the information in a resource in the server
  // This is very rarely ever used
})
//etc.
```

| Sending methods                                   | Description                                             |
|---------------------------------------------------|---------------------------------------------------------|
| res.sendStatus(statusCode)                        | Sends a HTTP status code                                |
| res.json({ message: "error"})                     | Sends json. .json only accepts an object.               |
| res.download("./fileToDownload.txt")              | Sends file to be downloaded.                            |
| res.send("html")                                  | The Content-Type header is set to text/html by default. |
| res.sendFile(path.join(__dirname, "/index.html")) | Renders html file in the browser                        |
| res.redirect('/newURL')                           | Redirects the client to a new URL.                      |
| res.end()                                         | Ends the response.                                      |

Your http methods need to return something, even an empty response, to indicate that the request was successfully handled. You can use `res.send("GET / handled successfully")`

#### Parameters
Parameters are data sent through the URL. This can include regular parameters like `/api/test/${id}` or query parameters like `/api/test?id=${id}`

```javascript
// Regular parameters
app.get("/api/test/:id", (req, res) => {
  const id = req.params.id
})
```

```javascript
// Query parameters
app.get("/api/test", (req, res) => {
  const id = req.query.id
})
```

- Often times parameters are set to `.toLowerCase()` to make them case insensitive. .toLowerCase is used over .toUpperCase because it is slightly faster.

#### Routers
Routers are used to help you organize your routes and the code for those routes.

In your main express file (usually server.js) you need to add:

```javascript
// In server.js. There is more to server.js
const api = require("./routes/index.js") // The exported app from index.js.

// Middleware
app.use("/api", api) // If the route uses /api it sends the endpoint to the api variable which is a separate Router in index.js.
```

```javascript
// In ./routes/index.js
const router = require("express").Router()

const tipsRouter = require("./tips") // The exported .Router() from tips.js

// Middleware
router.use("/tips", tipsRouter) // If the path is /api/tips send the endpoint to the tipsRouter

modules.exports = router
```

```javascript
// In ./routes/tips.js
const tipsRouter = require("express").Router()

tipsRouter.get("/", (req, res) => { // This path is /api/tips/
  res.send("The path is /api/tips")
})

module.exports = tipsRouter
```

#### Middleware Functions

```javascript
const middleware = (req, res, next) => {
  console.log(`Middleware function: ${req.method} with the ${req.get('Content-Type')}`)
  next() // Used to call the next middleware
}

app.use(middleware)
```

#### View Engines
View engines allow you to change the html from the server before it is sent.

This allows you to keep your view and your controller separated.

##### Handlebars

```javascript
const handlebars = require("express-handlebars")

app.engine("handlebars", handlebars()) // Sets the template engine which tells express how to render templates of a specific type
app.set("view engine", "handlebars") // Sets the default template engine defined in the first arg of app.engine()
  // This is the default template engine when not specifying an extension.

let view = './index.handlebars' // To specify which template engine to use(not the default) you have to make the extension the same name as the first arg into app.engine.
view = './index.html' // Or to use the default view engine set

const locals = {
  title: "Page title",
  items: [
    {firstName: "Ryan", middleInitial: "M", lastName: "Sheehy"},
    {firstName: "Bob", middleInitial: "B", lastName: "Bobby"},
  ],
  user: { // If you want to use user authentication
    name: "John Doe"
  }
}
app.render(view, locals, (err, html) => { // You use render in order to replace variables set inside your view file
  if(err){
    // handle error
    return
  }
  // use the rendered html
})

// Or you can use render to send data
app.get("/", (req, res) => {
  res.render('./public/index.html', locals)
  // This will send the rendered(with handlebars) html
})
```

View File Example:

```HTML
<!DOCTYPE html>
<html>
    <head> <!-- Contains metadata -->
        <title>{{title}}</title>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body> <!-- Contains the visible content -->
    {{#if user}}
      <p>Welcome {{user.name}}</p>
    {{/if}}
    <p>My name is {{firstName}} {{middleInitial}}. {{lastName}}.</p>
    <p>Here are my friends: </p>
    <ul>
      {{! This is a comment}}
      {{#each items}}{{! This loops through the locals}}
        {{#if @index 'greater' 0}}
          <li>{{firstName}} {{middleInitial}}. {{lastName}}.</li>
        {{/if}}
      {{/each}}
    </ul>
    </body>
</html>
```

#### Front end and Back end
Usually the front end is put in the public folder.

The front end should use `/` for any html links or server calls. Do not use `./`

The server should send the html page when getting `/` path.
### jest
Used for tests inside node.

Tests are used to test your code usually before sending them towards production. Install jest as a dev package.

Tests are usually done in small units(Unit Testing) so that if one test fails then you know where some code is broken.

In your package.json add
```javascript
"script": {
  "test": "jest"
}
```

`npm test` will now run jest and thus all of your tests.

To run a test file individually you can run `npx jest --testPathPattern=./filePath/file.test.js`

In order to create tests they have to be named `fileName.test.js`

```javascript
describe("test title" () => {
  test("test description", () => {
      // JS code tests
      expect(/*Code to be run*/).toBe(/*Weather the output of expects ===(strictly equals) this code.*/)
        // or
      expect(/*Code to be run*/).toEqual(/*Checks for structural equality. Compares the contents of two objects or arrays*/)
      expect(/*object*/).toBeInstanceOf(/*Class. Checks if the object is an instance of that Class.*/)
  })
  it("test description", () => {
    // This is the same thing as test
  })
})
```

- expect is used instead of if statements to make code cleaner and less lines.
- Each test/it is run in a separate instance so if an error is thrown in one of them it will still run the other tests/its.

### mysql2

```javascript
const mysql = require("mysql2")

const db = mysql.createConnection(
  {
    host: 'localhost',
    user: 'root',
    password: 'your_password',
    database: 'database_name'
  },
  console.log("Connected to the database.")
)

db.query(`SELECT * FROM table_name;`, (err, results) => {
  console.log(results)
})
```

#### mysql2 with Promises

```javascript
const mysql = require("mysql2/promise")

const db = mysql.createPool(
  {
    host: 'localhost',
    user: 'root',
    password: 'your_password',
    database: 'database_name'
  },
  console.log("Connected to the database.")
)

async function asyncQuery(){
  try{
    const [results, ] = await db.query(`SELECT * FROM table_name;`)
    return results
  }catch(error){
    console.error(error)
  }
}
```

#### Prevent SQL Injections
You can use the `?` in you SQL query to prevent SQL injections.

```javascript
async function unsafe(){
  const unsafeName = "' OR 1 = 1; DROP TABLE users; --" // SQL Injection
  const query = `SELECT * FROM users WHERE name = '${unsafeName}';`
  const [results, ] = await db.query(query)
  return results
}
```

```javascript
async function safe(){
  const firstName = "' OR 1 = 1; DROP TABLE users; --" // SQL Injection
  const lastName = "Sheehy"
  const query = `SELECT * FROM users WHERE first_name = ? AND last_name = ?;`
  const [results, ] = await db.query(query, [firstName, lastName])
  return results
}
```

### dotenv
Used to work with environment variables so that you don't have your passwords or keys stored in plane text.

Environment variables are variables that are local on your server or computer. Usually environment variables are all capitalized.

When deploying code on a server you can set that server to have specific environment variables.

Dotenv loads environment variables from a `.env` file into `process.env`. `.env` needs to be put into `.gitignore` so that it doesn't get pushed.

```javascript
// This sets up dotenv
require("dotenv").config()

console.log(process.env.API_KEY)
```

Example of `.env` file:

```
# These are comments
API_KEY=08fe01a78943266193fc7a23625f68fa
DB_PASSWORD=password
```

### bcrypt
Used to hash passwords. Bcrypt automatically creates the salt.

```javascript
const bcrypt = require('bcrypt')
```

#### Creating a Hash

```javascript
const saltRounds = 14 // Number of times the hash is applied. This sets the time to make the hash
// The salt Rounds are exponential. 2^saltRounds.
  // As computational power increases the salt rounds need to increase

bcrypt.hash(`password`, saltRounds, (err, hash) => {
  if(err){
    console.error(err)
    return
  }
  console.log(`Hashed password: ${hash}`)
})

// You can also use await
let hash = await bcrypt.hash(`password`, saltRounds)

// You can also use sync
let hash = bcrypt.hashSync(`password`, saltRounds)

```

#### Comparing a Password

```javascript
const hash = `$2b$07$i7vcjUJXJbczMVmbiJiQBOHEtZHk/N93Sh1H862iC9iKxVqIveihG`
// $ version of hash $ salt rounds $ 22 character salt and then 31 character hash
const password = `password`

bcrypt.compare(password, hash, (err, result) => {
  if(err){
    console.error(err)
    return
  }
  // Result is true or false
  console.log(`Is password correct? ${result}`)
})

// You can use async/await
let isPassword = await bcrypt.compare(password, hash)

// You can use sync
let isPassword = bcrypt.compareSync(password, hash)
```