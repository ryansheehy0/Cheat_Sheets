[Home](./README.md)

# JavaScript Under the Hood

## Table of Contents

<!-- TOC -->

- [JavaScript Under the Hood](#javascript-under-the-hood)
  - [Table of Contents](#table-of-contents)
  - [Todo](#todo)
  - [Call stack](#call-stack)
    - [Example 1](#example-1)
    - [Example 2](#example-2)

<!-- /TOC -->

## Todo
- global execution context and a function execution context
- When is the function execution context created
- What is stored in the function execution context
- call stack
- callback queue
- stack vs a queue in terms of LIFO and FIFO
- Asynchronous code and event loop
- higher order functions
- lexical environment
- encapsulated variables
- factory function
- inheritance and composition design

Javascript is single threaded. A thread has a call stack and memory heap.

## Call stack
  - stack of functions to be executed. At the bottom is always the Global Execution Context.
  - Manages execution context

LIFO - Last in first out. The last thing is is going to be the first thing out. Like a stack of plates where you take one from the top.
FIFO - First in first out. The first thing is is going to be the first thing out. Like a queue of people. The person who was first in line gets pulled out first.

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