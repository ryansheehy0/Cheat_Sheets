[Home](./README.md)

# JavaScript Under the Hood
Javascript is single threaded language. The thread has a call stack and memory heap. This cheat sheet goes through how those things work.

## Table of Contents

<!-- TOC -->

- [JavaScript Under the Hood](#javascript-under-the-hood)
  - [Table of Contents](#table-of-contents)
  - [Question](#question)
  - [Todo](#todo)
  - [- call stack](#--call-stack)
  - [LIFO/FIFO](#lifofifo)
  - [Call Stack](#call-stack)
    - [Example 1](#example-1)
    - [Example 2](#example-2)
  - [Callback Queue](#callback-queue)
  - [Event Loop](#event-loop)
  - [Global and Function execution context](#global-and-function-execution-context)

<!-- /TOC -->

## Question
Why can't javascript be multithreaded especially for something like node?

## Todo
- global execution context and a function execution context
- When is the function execution context created
  - When a new function is invoked
- What is stored in the function execution context
  - Local variables to that function
- call stack
  -
- callback queue
- stack vs a queue in terms of LIFO and FIFO
  - Stack is LIFO
  - Queue is FIFO
- Asynchronous code and event loop
- higher order functions
- lexical environment
- encapsulated variables
- factory function
- inheritance and composition design
- 'use strick' in the top of the js file


## [LIFO/FIFO](#table-of-contents)
**LIFO** - Last in first out.
- The last thing added is going to be the first thing out.
- Like a stack of plates where you take one from the top.

**FIFO** - First in first out.
- The first thing added is going to be the first thing out.
- Like a queue of people. The person who was first in line gets pulled out first.

## [Call Stack](#table-of-contents)
The call stack is LIFO and is a list of functions that need to be ran. The bottom is always the Global Execution Context.

### Example 1

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

### Example 2
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

## Callback Queue
The callback queue is a queue of functions waiting to be executed.

The output of the callback queue goes into the callback stack.

## Event Loop
Queue of data
There is a predefined list of events that happen when something happens. Like clicking a button sends a click event and adds that event to the event bus.

Mimics multithreaded behaviro

## Global and Function execution context
- global execution context and a function execution context

setTimeout(() -> {
  console.log("timeer")
}, 0)

console.log("outer")

// "outer" will always be printed before the timeout.
  // This is because the setTimeout is placed on the event loop and waits until all other code is finished.