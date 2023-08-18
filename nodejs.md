[Home](./README.md)

# NodeJS
NodeJS is used to run JavaScript outside of the browser.

Somethings work differently when using JS in NodeJS then in the browser. This cheat sheet will cover those differences.

## Table Of Contents
- [Questions](#questions)
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
- [Packages](#packages)
  - [Inquirer](#inquirer)
  - [Express](#express)
    - [Express HTTP Methods](#express-http-methods)
    - [Express Get](#express-get)
    - [View Engines](#view-engines)
      - [EJS](#ejs)
  - [Jest](#jest)

## Questions
<!--
? callback functions
? How to structure package.json files?
? npm init
? What is the difference between console in node and console in the browser?
? What are environment variables?
? What are all the different events?
? How can you write to files or create a new file?
? Do you have to make it a async function when returning a promise
? Does inquire have to return a Promise
? What are ports?
? What is local host?
? What is the HTTP protocol?
-->

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

## Packages

|          |                                                        |
|----------|--------------------------------------------------------|
| inquirer | Used to simply get user input from the terminal        |
| express  | Simplifies HTTP-related tasks usually for making APIs. |
| jest     | Used for tests inside node.                            |

### Inquirer
Used to simply get user input from the terminal.

```javascript
const inquirer = require('inquirer')

async function askQuestion(question, answerName, validationFunction){
  return new Promise((resolve, reject) => {
    inquirer.prompt([
      {
        type: 'input',
        name: answerName,
        message: question,
        validate: validationFunction,
      }
    ])
    .then(answer => {resolve(answer)})
    .catch(error => {reject(error)})
  })
}
```

### Express
Simplifies HTTP-related tasks usually for making APIs. It's a framework for handling http requests.

```javascript
const express = require("express")
const path = require("path")

const app = express()

// Settings
const settingName = "view engine"
const settingValue = "ejs"
app.set(settingName, settingValue)

// Middleware. Middleware functions are functions that can intercept and process incoming requests before they reach route handlers

app.use(express.json()) // Parses the body with json
app.use(express.static('public')) // Setting for serving static files from the public folder. You can directly call the file. Ex: localhost:3000/images/image.jpg

// HTTP Methods

// Listen
const port = 3000
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
  console.log("Test") // Outputs to the terminal of the server
})
app.post("/", (req, res) => {
  const data = req.body
})
app.put("/", (req, res) => {})
app.delete("/", (req, res) => {})
app.patch("/", (req, res) => {})
//etc.
```

| Sending methods                                   | Description                                             |
|---------------------------------------------------|---------------------------------------------------------|
| res.sendStatus(statusCode)                        | Sends a HTTP status code                                |
| res.json({ message: "error"})                     | Sends json                                              |
| res.download("./fileToDownload.txt")              | Sends file to be downloaded.                            |
| res.send("html")                                  | The Content-Type header is set to text/html by default. |
| res.sendFile(path.join(__dirname, "/index.html")) | Renders html file in the browser                        |
| res.redirect('/newURL')                           | Redirects the client to a new URL.                      |

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

#### View Engines
View engines allow you to change the html from he server before it is sent.
- EJS and Pug are popular view engine libraries

`app.set("view engine", "ejs")` sets the view engine to EJS. Need to run `npm install ejs` before this can work.

##### EJS
- .html files need to be changed to .ejs
- The .ejs files need to be placed in the views folder
- Inside .ejs files you can output into the html by using `<%= %>`
  - Ex: `<p>2 plus 2 equals <%= 2 + 2 %></p>`

```javascript
res.render("index") // Uses the view engine to render html in the browser.

res.render("index", { text: "world" })
  // To access this object in your .ejs file use <%= key %>
    // Ex: <%= text %>
```

### Jest
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

## Path
`const path = require("path")`

## Node-fetch
Allows you to use the fetch function in node
`const fetch = require('node-fetch')`