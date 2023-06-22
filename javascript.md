[Home](./README.md)

# JavaScript
JavaScript is the only language that can be run in the browser.

## Table of contents

## Comments

```
// Inline comment
/*
    Multi-line comment
    No nested multi-line comments
*/
```

## Primitive Data types
- Dynamically typed. A variable can be assigned to multiple types.
- `typeof operand` can be used to get a string of the type
    - undefined
        - Is an uninitialized value
    - boolean
        - Includes true or false
        - Something is false if it has the values of 0, -0, On, "", null, undefined, NaN, or false.
        - Often start with the words is, has, or should.
    - string
    - number
        - Includes ints, floats, NaN, and Infinity
    - object
        - null. The absence of an object.
        - key-value pairs
        - Object types: object, date, array, string, number, boolean.
    - function
    - symbol
        - `Symbol()` or `Symbol("description")
        - Unique(Symbols cannot equal anything else) and immutable.
    - bigints
        - Support integers of arbitrary size
        - `123n` or `BigInt(123)`

## sets
- Only can store unique values. If you attempt to add a duplicate it will be ignored.
- There is no specific ordering.
- `new Set()`
- `set.add(value)`, `set.delete(value)`, `set.has(value)`, `set.size`, `set.clear()`

## Variables
var - Can be used through your whole program

let - Only used within the scope of where you declared it

const - Variable that can never change

- A refresh in the browser clears all variables.
- camelCase is most commonly used

```
function example() {
  var x = 10; // function scope
  let y = 20; // block scope

  if (true) {
    var x = 30; // same variable, modifies the outer x
    let y = 40; // different variable, block-scoped
    console.log(x); // 30
    console.log(y); // 40
  }

  console.log(x); // 30
  console.log(y); // 20 (outer y, unchanged)
}

example();
```

## Strings
Strings can start with "s, 's, or `s

Escape seqences: \\", \\', \\`, \\ \\
- \b backspaces
- \f form feed
- \n new line
- \r Carriage return
- \t tab
- \v vertical tab

+s can be used to concatenate strings

Strings are immutable. Once a string is created its value cannot be changed. If the value is changed what is happening is that a new string is being made and assigned.

### String methods
- `.length`
    - Size of the string
- `.slice(start, end)` or `.slice(start)` 
    - Extracts part of a string.
    - The index of the string starts at 0.
    - The start is inclusive while the end is not.
    - Ex: `let text = "Apple, Banana, Kiwi"; let part = text.slice(7,13); //part is "Banana"`
    - slice allows for negative numbers. The last character is -1.
    - If only the start is specified then the rest of the string is sliced out.
- `.substr(start, length)` or `.substr(start)`
    - Extracts part of a string from the start(inclusive) to the length
    - Negative numbers can be used.
- `.replace(/regex/, replaced_string)` or `.replace(searching_string, replaced_string)`
    - /regex/g can be used to replace multiple times instead of just once
- `.toUpperCase()` or `.toLowerCase()`
- `.trim()` or `.trimStart()` or `.trimEnd()`
    - Used to remove the white space from start and/or end of a string
- `.split(string)` or `.split(/regex/)`
    - Converts a string to an array by splitting along the string arg. Doesn't include the splitting string arg.
- `.charAt(index)`
    - Gets the character at that index. If there is no character there then it returns an empty string.
    - Cannot take negative numbers.

## Arrays
Arrays allow you to store several pieces of data in the same place. Elements can be any data type and arrays are mutable.

### Useful array functions
- `.length`
- `.join(string_separator)`
    - Converts an array to a string with the string separators between each element.
- `.pop()`
    - Removes the last element and returns what was popped.
- `.push(value)`
    - Adds the value to the end of the array.
- `.shift()`
    - Removes the first element and shifts the array to the left by one. Returns what was shifted out.
- `.unshift(value)`
    - Adds the value to the beginning of the array.
- `.concat(array)`
    - Creates a new array by merging the adding the array arg to the array that was called upon.
- `.flat()`
    - Reducing a multi-dimensional array to one array.
    - Ex: [[1,2],[3,4]] -> [1,2,3,4]
- `.splice(index where new elements should be added, how many elements should be removed, new elements to be added)`
    - Elements are added before the index specified
    - Can be used to remove elements in an array
- `.forEach(function)`
    - Runs the function for each element in the array. 
    - The args that forEach passes are value/element, key/index, and array
- `.map(function)`
    - Performs a function for each element in an array, then stores the returned values in a new array.
    - The args that forEach passes are value/element, key/index, and array

```
const fruits = ["Banana", "Orange", "Apple", "Mango"]
fruits.splice(2, 0, "Lemon", "Kiwi")
console.log(fruits)
//Outputs: [ "Banana", "Orange", "Lemon", "Kiwi", "Apple", "Mango" ]

fruits = ["Banana", "Orange", "Apple", "Mango"]
fruits.splice(1, 1)
console.log(fruits)
//Outputs: [ "Banana", "Apple", "Mango" ]
```

- `.slice(start, end)` or `.slice(start)`
    - Slices out a piece of an array into a new array without modifying the existing the array.

## Equality operators
- `===` `!==` strict operator
    - Doesn't do the type conversion
- `==` `!=` 
    - Attempts to convert both values to a common type. Allows type coercion.
    - <, >, <=, >= attempts to convert values

```
3 === 3 // true
3 === '3' // false
3 == 3 // true
3 == '3' // true
```

## Switch block

```
let x = 10
switch(x) {
    case 1:
        console.log("This is a 1.")
        break
    case 2:
        console.log("This is a 2.")
        break
    default:
        console.log("This is greater than 2.")
        break
}
```

## Functions
- If you don't return anything then the return value is undefined

```
function func_name1(arg1, arg2) {}

func_name2 = (arg1, arg2) => {}

// Rest operator. Used to allow a function to have a variable number of args.
func_name3 = (...args) => {
    console.log(args[0], args[1])
}
```

## Useful functions

|                                          |                                                                                                          |
|------------------------------------------|----------------------------------------------------------------------------------------------------------|
| console.log("x is " + x)                 | Prints to the console.                                                                                   |
| prompt("Message")                        | Shows a pop up with message and allowing user input.                                                     |
| Math.PI                                  | 3.141592653589793                                                                                        |
| Math.abs(num)                            | Absolute value                                                                                           |
| Math.random()                            | Returns a random floating point num between 0 and 1. Can return a 0, but not a 1.                        |
| Math.floor(num)                          | Rounds down to the nearest whole number                                                                  |
| Math.floor(Math.random() * (num + 1))    | Picks a random integer from 0 to num.
| Math.ceil(num)                           | Rounds up to the nearest whole number                                                                    |
| .toFixed(number of decimal places)       | Rounds to the number of decimal places.                                                                  |
| parseInt(str) or parseInt(str, base num) | Converts a string to an int. If it can't then it returns NaN                                             |
| setTimeout(function, milliseconds)       | The function runs after the delay time in milliseconds. Other code can run while waiting for setTimeout. |

### Fetch
Used to fetch data from a server.

```
fetch("URL", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({ key1: "value1", key2: "value2"})
})
    .then(response => response.json()) // asynchronously returns an object from the json string
    .then(data => {
        console.log(data)
    })
    .catch(error => {
        console.log(error)
    })
```

## Objects
Objects store value in a key-value pair.

```
let testObj = {
    "A food": "hamburger",
    "drink": "water",
}

let test2Obj = {
    food: "hamburger",
    drink: "water",
}

console.log(testObj.drink) // water
// if the key contains a space then you must use this syntax
console.log(testObj["A food"]) // hamburger
```

- You can delete a property from an object
    - Ex: `delete testObj.drink`
- You can check if an object has a property with `.hasOwnProperty("property")`
    - Ex: `testObj.hasOwnProperty("A food")`

### JavaScript Object Notation(JSON)
- The last key-value pair cannot end with ,s
- Convert JSON to an object
    - `JSON.parse(json)`
    - You can convert asynchronously with `json.json()`

```
const json = '{"first name": "Ryan", "last name": "Sheehy"}'
const obj = JSON.parse(json, (key, value) => {
    if(key === "last name"){
        return "M. " + value
    }
    return value
})
console.log(obj)
```

- Convert an object to JSON
    - `JSON.stringify(obj)`

### Spread operator
- Used to spread out an array or an object

```
const numbersOne = [1, 2, 3];
const numbersTwo = [4, 5, 6];
const numbersCombined = [...numbersOne, ...numbersTwo]; 

const numbers = [1, 2, 3, 4, 5, 6];
const [one, two, ...rest] = numbers; 
console.log(one) // 1
console.log(two) // 2
console.log(rest) // 3, 4, 5, 6

const obj1 = {
  firstName: "Ryan",
  lastName: "Sheehy",
}
const obj2 = {
  firstName: "Ryan",
  lastName: "Sheehy",
}
const obj3 = {...obj1, ...obj2} 
```

## Template literals
Used to make complete string with embedded JS.
- Starts with \`s
- It allows you to have multi-line strings with a newline inserted.

```
let person = {
    name: "Ryan Sheehy",
    age: "21",
}
console.log(`Hello, my name is ${person.name}!
I am ${person.age} years old.`)
```

## Import and Export
Use `export` to export the var/function
    - Ex: `export const name = "Ryan Sheehy"`
    - There can be a default export for a file. There can only be 1 default export.

```
import { name } from "./filepath"
// If it is a .js file you don't have to put .js at the end

//Import everything
import * as objectName from "./filepath"

let x = 10
default export x

// In order to import the default export you use
import Name from "./filepath"
```

## Error handling
Used to keep the code running even when there is an error.

```
try{
    // Code that may throw an error
    if( variable ){
        throw "Custom error message." // The "Custom error message." is in error and not error.name or error.message
    }
}catch(error) {
    // These are the only 2 keys in an error
    console.log(error.name)
    console.log(error.message)
}finally{
    // Code that runs after the try catch regardless of what the try catch does
}
```

## Promises
Used to handle asynchronous(code can be run in parallel) operations.

```
let promise = new Promise((resolve, reject) => {
    let x = 1 + 1
    if( x == 2 ){
        resolve("Success")
    }else{
        reject("Failed")
    }
})

promise.then((message) => {
    // then runs if the promise returns a resolve
    console.log(message) // "Success"
}).catch((message) => {
    // catch runs if the promise returns a reject
    console.log(message) // "Failed"
}
```

## Async/Await
Used to make promises easier to work with. Only works with asynchronous functions.

```
async func_name = () => {
    await promise_function()
    // The code will wait until promise_function returns something. It just returns the resolved section and not the rejected section.
        // To get the rejected you can use .catch{}
}
```
