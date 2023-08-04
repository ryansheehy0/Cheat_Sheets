[Home](./README.md)

# NodeJS
NodeJS is used to run JavaScript outside of the browser.

Somethings work differently when using JS in NodeJS then in the browser. This cheat sheet will cover those differences.

## Table Of Contents

## Questions
- callback functions
- How to structure package.json files?
- npm init

## Getting Started
Run `node -v` to see what version of node you have. If you don't have node you can install it from [here].
You can run `node script.js` or `node script` to run a JS file.

### Node Package Manager(NPM)
NPM is used to install dependencies/packages for NodeJS code.

You can run `npm install <package>` to install your desired package.

Dependencies can be listed in a package.json file.
```
```

-  To install dependencies/package from a package.json file run `npm install`. 
    - This will create a folder called node_modules which has the JS code of the dependencies/package.

## Things that don't work
- window global variable
- alert, prompt, and confirm

## this keyword
- In order to use the this keyword you have to be inside a function.

## Global Variables

|         |                                                      |
|---------|------------------------------------------------------|
| global  |                                                      |
| process | Info and controls over the current node environment. |
| console | Log info to the console.                             |
| module  |                                                      |
| Buffer  | Used to handle binary data.                          |

## Event Emitter

## Arguments

## File System
fs

## Packages

|          |                                                 |
|----------|-------------------------------------------------|
| inquirer | Used to simply get user input from the terminal |

