[Home](./README.md)

# NodeJS
NodeJS is used to run JavaScript outside of the browser.

Somethings work differently when using JS in NodeJS then in the browser. This cheat sheet will cover those differences.

## Table Of Contents

## Questions
- callback functions
- How to structure package.json files?
- npm init
- What is teh difference between console in node and console in the browser?
- What are environment variables?
- What are all the different events?
- How can you write to files or create a new file?

## Getting Started
Run `node -v` to see what version of node you have. If you don't have node you can install it from [here](https://nodejs.org/en).

You can run `node script.js` or `node script` to run a JS file.

### Node Package Manager(NPM)
NPM is used to install dependencies/packages for NodeJS code.

|                           |                                                                                                             |
|---------------------------|-------------------------------------------------------------------------------------------------------------|
| `npm init`                | Sets up a package.json file in order to keep track of needed dependencies.                                  |
| `npm init -y`             | Sets up a package.json file with the default settings.                                                      |
| `npm install <package>`   | Installs the package for your project. Puts it in your package.json                                         |
| `npm install <package>@8.2.4`   | Installs the package with the version 8.2.4 for your project. Puts it in your package.json            |
| `npm uninstall <package>` | Uninstalls the package for your project.                                                                    |
| `npm install`             | Installs all the dependencies if there is a package.json file and if the packages aren't already installed. |

package-lock.json locks the versions of the packages so that new version don't brake your code.

#### Importing
To import the exported variable you can do `const module = require("./filepath.js")`

In order to import from a package you do `const package = require("packageName")`

#### Exporting
To export you use the module.exports object
```
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

|         |                                                                                       |
|---------|---------------------------------------------------------------------------------------|
| global  | Global for all files in your program. Like the window global variable in the browser. |
| process | Info and controls over the current node environment.                                  |
| console | Log info to the console.                                                              |
| module  |                                                                                       |
| Buffer  | Used to handle binary data.                                                           |

### Process
`process.platform` get what platform the node is running on like linux.
`process.env.NAME` get the environment variable called NAME

process.argv is an array that contains the command-line arguments.
process.argv[0] is the path to node
process.argv[1] is the path to the executable
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
```
const { EventEmitter } = require('events)
const eventEmitter = new EventEmitter

eventEmitter.emit("eventName")
```

### Receiving Events
```
eventEmitter.on("eventName", () => {
})
```

## File System
`const fs = require('fs')` or with premisses `const fs = require('fs').promises`

### Reading to Files

```
const encodingType = "utf8"

// Blocking/Sync
const file = fs.readFileSync("filepath.txt", encodingType)

// Non-Blocking
fs.readFile("filepath.txt", encodingType, (error, file) => {// function when file is loaded})

// Asynchronous/Promises
async function loadFile() {
    const file = await fs.readFile("filepath.txt", encodingType)
}
```

### Writing to Files
```
fs.writeFile("./filepath.txt", "Written data", error => {error ? console.log(error) : false})
```

### Appending to Files
```
fs.appendFile("./filepath.txt", "Written data", error => {error ? console.log(error) : false})
```

## Packages

|          |                                                        |
|----------|--------------------------------------------------------|
| inquirer | Used to simply get user input from the terminal        |
| express  | Simplifies HTTP-related tasks usually for making APIs. |