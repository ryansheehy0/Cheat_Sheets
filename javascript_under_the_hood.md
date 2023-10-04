[Home](./README.md)

# JavaScript Under the Hood
Javascript is single threaded language. The thread has a call stack and memory heap. This cheat sheet goes through how those things work and other things on how javascript works under the hood.

## Table of Contents

<!-- TOC -->

- [JavaScript Under the Hood](#javascript-under-the-hood)
  - [Table of Contents](#table-of-contents)
  - [LIFO/FIFO](#lifofifo)
  - [Call Stack](#call-stack)
    - [Example 1](#example-1)
    - [Example 2](#example-2)
  - [Callback Queue and Event Loop](#callback-queue-and-event-loop)
  - [Global and Function Execution Context](#global-and-function-execution-context)
  - [Use Strick](#use-strick)

<!-- /TOC -->

## [LIFO/FIFO](#table-of-contents)
**LIFO** - Last in first out.
- The last thing added is going to be the first thing out.
- Like a stack of plates where you take one from the top.

**FIFO** - First in first out.
- The first thing added is going to be the first thing out.
- Like a queue of people. The person who was first in line gets pulled out first.

## [Call Stack](#table-of-contents)
The call stack is LIFO and is a list of functions that need to be ran. The bottom is always the Global Execution Context.

### [Example 1](#table-of-contents)

```javascript
function first(){console.log("first")}
function second(){console.log("second")}
function third(){console.log("third")}

first()
second()
third()
```

         | Call Stack |
         |------------|
third -> | second     | -> first
         | Global EV  |

### [Example 2](#table-of-contents)
When you have functions inside functions it is added to the call stack.

```javascript
function first(){
  console.log("first")
  second()
}

function second(){
  console.log("second")
  third()
}

function third(){
  console.log("third")
}

first()
```

| Call Stack |
|------------|
| third      |
| second     |
| first      |
| Global EC  |

## [Callback Queue and Event Loop](#table-of-contents)
When an `async` function is called it runs synchronously like any other function. If an `await` is encountered, it passes the code to the webAPI or the NodeAPI.

The webAPIs or the NodeAPIs run in a different threads and are called when async operations need to be performed.

When the async operation finishes, like the timer in `setTimeout` or `fetch` gets back data, the callback function(with async, the code after the await) is added to the callback queue.

The event loop checks if the callback stack is empty. If it is empty it checks for the next callback function in the event queue. It then puts the 

## [Global and Function Execution Context](#table-of-contents)
The global execution context is the outermost scope in JS.

The function execution context is created when a function is invoked and variables declared in the function can only be used in the function.

## [Use Strick](#table-of-contents)
Use strick is used to convert bad syntax to errors.

To use use strick you can either put `"use strick"` at the top of your js file or put `"use strick"` at the top of functions to just use strick for that function.

- Can't use un-declared variables.
  - You have ot first create a variable with var, const, or let
- You can't delete a variable
  - Ex: `const x = 5; delete x;` will throw an error
- No duplicate argument names in functions
- `this` is undefined for functions that aren't methods
- Can't use `with` or `eval` keyword