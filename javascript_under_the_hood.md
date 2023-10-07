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
  - [Useful terms](#useful-terms)
  - [Closures](#closures)
    - [Var/Let strick question](#varlet-strick-question)
  - [Big O Notation](#big-o-notation)

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
[This](https://www.youtube.com/watch?v=8aGhZQkoFbQ&list=WL&index=3) is a good resource.

When an `async` function is called it runs synchronously like any other function. If an `await` is encountered, it passes the code to the webAPI or the NodeAPI.

The webAPIs or the NodeAPIs run in a different threads and are called when async operations need to be performed.

When the async operation finishes, like the timer in `setTimeout` or `fetch` gets back data, the callback function(with async, the code after the await) is added to the callback queue.

The event loop checks if the callback stack is empty. If it is empty it checks for the next callback function in the event queue. It then puts that function in the callback stack.

The synchronous functions always have higher priority than any function in the callback queue.

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

## [Useful terms](#table-of-contents)

| Term                   | Definition                                  |
|------------------------|---------------------------------------------|
| Higher order functions | Functions with other functions as arguments |
| Shallow copy           | Pass by reference                           |
| Deep copy              | Pass by value                               |
| Lexical Envurornemrn | |

## [Closures](#table-of-contents)
Closures are functions that are returned from another function, that allow you to access private variables in the outer function.

When a function is returned a closure, in the backend, is made which holds the private variables.

```javascript
function bankAccount() {
  const checking = 400
  const savings = 1000

  return {
    displayFunds: function () {
      console.log(`You have $${checking} in your checking account and $${savings} in your savings account`)
    },
  }
}
```

Factory functions are like closures, but are given arguments.

### [Var/Let strick question](#table-of-contents)

```javascript
// var is scoped to the global scope therefore it doesn't change closures
// If i were let it would be scoped to the for loop and would have its own closure.
  // If it was let it would be 0, 1, 2
for(var i = 0; i < 3; i++){
  const log = () => {
    consol.log(i)
  }

  setTimeout(log, 100)
}

// This will output 3 3 3
```

## [Big O Notation](#table-of-contents)
Because an increasingly complex computer can run any algorithm faster, in order to compare algorithms we use a standard notation called Big O Notation.

Big O Notation removes any constants and only accounts for the number of inputs so you don't have to worry about different computers.

Big O notation uses the syntax of O().

This is the efficiency in order of worst to best when n is very large.
  - O(n!), O(2^n), O(n^2), O(n log n), O(n), O(log n), O(1)

The Big O of a for loop is O(n)

The Big O of a nested for loop in another for loop is O(n^2)

Big O notation is always the worst case scenario