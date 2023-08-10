[Home](./README.md)

# JavaScript
JavaScript is the only language that can be run in the browser.

## Table of Contents
- [Comments](#comments)
- [Primitive Data Types](#primitive-data-types)
- [Sets](#sets)
- [Variables](#variables)
- [Strings](#strings)
    - [String Functions](#string-functions)
- [Arrays](#arrays)
    - [Array Functions](#array-functions)
- [Equality Operators](#equality-operators)
- [Switch Block](#switch-block)
- [Functions](#functions)
- [Useful Functions](#useful-functions)
    - [Fetch](#fetch)
        - [Optional Fetch Argument](#optional-fetch-argument)
- [Objects](#objects)
    - [For In](#for-in)
    - [JavaScript Object Notation(JSON)](#javascript-object-notationjson)
    - [Spread Operator](#spread-operator)
- [Template Literals](#template-literals)
- [Import and Export](#import-and-export)
- [Error Handling](#error-handling)
- [Promises](#promises)
- [Async/Await](#asyncawait)
- [DOM Manipulation](#dom-manipulation)
    - [Accessing Elements](#accessing-elements)
    - [Modifying Elements](#modifying-elements)
    - [Creating and Appending Elements](#creating-and-appending-elements)
    - [Event Handling](#event-handling)
        - [Commonly Used Events](#commonly-used-events)
        - [Default Events](#default-events)
    - [Traversing the DOM](#traversing-the-dom)
- [This](#this)
- [Timing](#timing)
- [+/-/++/-- Operators](#----operators)
- [Local/Session Storage](#localsession-storage)
- [Common APIs](#common-apis)
    - [DayJS](#dayjs)
- [URL of Webpage](#url-of-webpage)
    - [Redirect URL](#redirect-url)
- [Regex](#regex)

## Comments

```
// Inline comment
/*
    Multi-line comment
    No nested multi-line comments
*/
```

## Primitive Data Types
- Dynamically typed. A variable can be assigned to multiple types.
- By default all objects and array are pass by reference. In order to do a pass by value you have to use the spread operator.`[...array]` 
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

## Sets
- Only can store unique values. If you attempt to add a duplicate it will be ignored.
- There is no specific ordering.
- `new Set()`
- `set.add(value)`, `set.delete(value)`, `set.has(value)`, `set.size`, `set.clear()`

## Variables
`var` - Can be used through your whole function or program if declared outside a function.

`let` - Only used within the scope of where you declared it

`const` - Variable that can never change. Block-scope
    - You can still do array functions like `.pop` or `.push`

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

### String Functions
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
- `.contains("substring")`
    - Does the string contain the substring in it?

## Arrays
Arrays allow you to store several pieces of data in the same place. Elements can be any data type and arrays are mutable.

### Array Functions
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
- `.forEach(function)`
    - Runs the function for each element in the array. 
    - The args that forEach passes are value/element, key/index, and array
- `.map(function)`
    - Performs a function for each element in an array, then stores the returned values in a new array.
    - The args that forEach passes are value/element, key/index, and array
- `.filter(function(element))`
    - Filter loops through and array and allows you to remove elements
    - If the function returns false for that element then it gets removed.
```
// Keeps all the even numbers
let numbers = [1, 3, 4, 5, 5, 2]
numbers = numbers.filter((element) => {
    return element % 2 === 0
})
console.log(numbers)
```
- `.slice(start, end)` or `.slice(start)`
    - Slices out a piece of an array into a new array without modifying the existing the array.
- `.reduce((accumulator, item) => {}, startingValue)`
    - Takes an array and reduces it to 1 value
    - The accumulator is set to the startingValue when starting to go through the function.
    - Whatever is returned from the function is what is set to the total for the next iteration
```
const prices = [10, 20, 30, 40]
const totalPrice = prices.reduce((total, price) => {
    return total + price
}, 0)
console.log(totalPrice)
```
- `.find(function)`
    - Used to find the first element that satisfies the given function.
- `.sort((a, b) => a - b)`
    - If the function returns a negative number "a" is sorted before "b"
    - If the function returns a positive number "b" is sorted before "a"
```
const numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5];

numbers.sort((a, b) => a - b);

console.log(numbers); // Output: [1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]

```

## Equality Operators
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

## Switch Block

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
    - Can be declared below their use. This is called hoisting and is unique to JS.
```
func() // Prints out Test
function func() {
    console.log("Test")
}
```

```
function func_name1(arg1, arg2) {}

const func_name2 = function(arg1, arg2) {}

const func_name3 = (arg1, arg2) => {}

const func_name4 = arg1 => {}

// Rest operator. Used to allow a function to have a variable number of args.
const func_name4 = (...args) => {
    console.log(args[0], args[1])
}
```

- When using the function keyword the `this` keyword is reset.
- When using the arrow function(=>) the `this` keyword is not reset.
    - The `this` keyword is most commonly used withing objects.
    - Avoid using arrow functions(=>) inside objects at least on the first layer.

- You can run a function immediately by doing
```
(function() {
    console.log("Function that ran immediately")
})()
```

## Useful Functions

|                                          |                                                                                                          |
|------------------------------------------|----------------------------------------------------------------------------------------------------------|
| console.log("x is " + x)                 | Prints to the console.                                                                                   |
| prompt("Message")                        | Shows a pop up with message and allowing user input.                                                     |
| alert("Message")                         | Shows an alert to the user. No user input.                                                               |
| confirm("Message")                       | Shows message to user and takes user input as true or false.                                             |
| Math.PI                                  | 3.141592653589793                                                                                        |
| Math.abs(num)                            | Absolute value                                                                                           |
| Math.random()                            | Returns a random floating point num between 0 and 1. Can return a 0, but not a 1.                        |
| Math.floor(num)                          | Rounds down to the nearest whole number                                                                  |
| Math.floor(Math.random() * (num + 1))    | Picks a random integer from 0 to num.
| Math.ceil(num)                           | Rounds up to the nearest whole number                                                                    |
| .toFixed(number of decimal places)       | Rounds to the number of decimal places.                                                                  |
| parseInt(str) or parseInt(str, base num) | Converts a string to an int. If it can't then it returns NaN                                             |

### Fetch
Used to fetch data from a server. Returns a promise of the response.

```
fetch("URL")
.then(response => response.json()) // asynchronously returns an object from the json string
.then(data => {
    console.log(data)
})
.catch(error => {
    console.log(error)
})
```

You can specify the headers that fetch uses.

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

#### Optional Fetch Argument

| method: | Description                     |
|---------|---------------------------------|
| GET     | Gets data from the server.      |
| PUT     | Updates data in the server.     |
| POST    | Creates new data in the server. |
| DELETE  | Deletes data in the server.     |

| credentials: | Description                                                 |
|--------------|-------------------------------------------------------------|
| same-origin  | Cookies/credentials only in request when same origin.   |
| include      | Cookies/credentials stored in request regardless of origin. |
| omit         | Excludes cookies and credentials                            |

Origin means the same URL, protocol, domain(.com, .net, etc), and port.

| cache: | Description                                      |
|--------|--------------------------------------------------|
| reload | Stop cacheing of data by the browser for that fetch.|

| redirect: | Description                      |
|-----------|----------------------------------|
| follow    | Automatically follows redirects. |
| manual    | Can manually handle redirects.   |
| error     | Error when there are redirects.  |


`headers:` are used to send additional information.
```
headers: {
    'Content-Type': 'application/json'
}
```

`body:` is where the data you want to send is stored such as JSON.

## Objects
Objects are used to store an unordered list of properties to describe one thing.

Literal object notation is an object created with key-value pairs.

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
- Objects can have functions. Methods are functions inside objects.
- Object.values(object) converts an object to an array where the keys are replaced with indices.
- Object.keys(object) gets an array of the keys of that object
- You can do object shorthand if the key and value are the same
```
const object = {
    test1: test1,
    test2: test2,
}
// Shorthand form
const object = {
    test1,
    test2,
}
```
- To get specific values from an object or array you can use this notation
```
const object = {
    key1: "value1",
    key2: "value2"
}
const array = ["ele1", "ele2"]

const { key1, key2 } = object
const [ var1, var2 ] = array

console.log(key1) // value1
console.log(key2) // value2
console.log(var1) // ele1
console.log(var2) // ele2
```

### For In
- You need to do [] when referencing properties in a for in loop in case the property has a space in it.

```
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(property + ": " + object[property]);
}
// "a: 1"
// "b: 2"
// "c: 3"
```

### JavaScript Object Notation(JSON)
- The last key-value pair cannot end with ,s
- Convert JSON to an object
    - `JSON.parse(json)`
    - You can convert asynchronously with `json.json()`

```
const json = '{"first name": "Ryan", "last name": "Sheehy"}'
const obj = JSON.parse(json, (key, value) => {
    if(key === "last name"){
        return "Mr. " + value
    }
    return value
})
console.log(obj) // "first name": "Ryan", "last name": "Mr. Sheehy"
```

- Convert an object to JSON
    - `JSON.stringify(obj)`
    - stringify has optional arguments for formatting.
        - `JSON.stringify(obj, null, 2)`

### Spread Operator
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

It can be used to create an array from something that isn't an array. `[...nonArray]`

## Template Literals
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

## Error Handling
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
Used to handle asynchronous(code can be run in parallel) operations. Can only return either a resolve or a reject.

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
    try{
        let variable = await promise_function()
        // The code will wait until the promise_function returns.
        let variable2 = await promise_function2()
    }catch(error){
        // If either promise_function or promise_function2 returns an error
    }
}
```

## DOM Manipulation
The DOM is the Document Object Model.

The `window` is an object that have internal functions and data that can be accessed. `document` is an object part of the window and is the DOM. `document` allows JavaScript to access different elements of the HTML page.

### Accessing Elements

|                                          |                                                            |
|------------------------------------------|------------------------------------------------------------|
| document.getElementById('id')            | Returns element with the id                                |
| document.getElementsByClassName('class') | Returns a collection of elements with the class            |
| document.getElementsByTagName('tag')     | Returns a collection of elements with the tag/element name |
| document.querySelector('selector')       | Returns the first element with the CSS selector            |
| document.querySelectorAll('selector')    | Returns a collection of element with the CSS selector      |

The selector in querySelector cannot start with a number therefore ids and classes should preferably start with letters.

### Modifying Elements

|                                            |                                                                           |
|--------------------------------------------|---------------------------------------------------------------------------|
| element.textContent = 'text'               | Sets text content of the element                                          |
| element.innerHTML = 'html'                 | Sets the html content of the element                                      |
| element.value = 'value'                    | Sets the value content of the element                                     |
| element.setAttribute('attribute', 'value') | Sets the attribute of the element                                         |
| element.style.property = 'value'           | Sets the CSS style property of the element                                |
| element.classList.add('class')             | Adds a CSS class to the element                                           |
| element.classList.remove('class')          | Removes a CSS class on the element                                        |
| element.classList.toggle('class')          | Toggles the presence of a CSS class on the element                        |
| element.dataset.name = "name"              | Searches the html attributes for data-name and sets its contents to name. |

### Creating and Appending Elements

|                                                      |                                                                    |
|------------------------------------------------------|--------------------------------------------------------------------|
| document.createElement('tag')                        | Creates a new element with the specified tag. Tag shoudn't have <>s|
| element.appendChild(newChild)                        | Appends a new child element to the given parent element            |
| element.append(child)                                | Appends a new child element. Very similar to appendChild           |
| parentElement.insertBefore(newChild, referenceChild) | Inserts a new child element before a specified reference element   |
| parentElement.removeChild(childElement)              | Removes a specified child element from its parent                  |

#### Insert Adjacent Element
`element.insertAdjacentElement("position", newElement)` or `element.insertAdjacentHTML("position", "html")`

| Position Name | Description    |
|---------------|----------------|
| afterbegin    | First child    |
| afterend      | After element  |
| beforebegin   | Before element |
| beforeend     | Last child     |

### Event Handling

|                                                     |                                                                                          |
|-----------------------------------------------------|------------------------------------------------------------------------------------------|
| element.addEventListener('event', eventFunction)    | Attaches an event listener to the element                                                |
| element.removeEventListener('event', eventFunction) | Removes an event listener from the element                                               |
| event.preventDefault()                              | Prevents the default event for an element. Certain elements have default events.         |
| event.stopPropagation()                             | Only have to worry if you have clickable elements inside clickable elements in the html. |

```
// To dynamically add listeners to dynamically added elements.
    // You cannot get the element when the element isn't created in the DOM
  document.querySelector("element already created by the dom").addEventListener("click", function(event){
    if(event.target.className.includes("dynamically created element's class")){
      //You can also use ids
      //Your event code here
    }
  })
```

#### Commonly Used Events

| Event         | Description                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------|
| click         | Element is clicked.                                                                           |
| dblclick      | Element is double clicked.                                                                    |
| load          | Fires when a resource and its dependent resources have finished loading.                      |
| mouseover     | Triggered when the mouse pointer enters an element.                                           |
| mouseout      | Triggered when the mouse pointer leaves an element.                                           |
| keydown       | Fired when a key is pressed down. eventFunction should have an event and the key is event.key |
| keyup         | Fired when a key is released. eventFunction should have an event and the key is event.key     |
| submit        | Fired when a form is submitted. Button needs type="submit" Also submits with the enter key.   |
| change        | Triggered when the value of an element changes.                                               |
| resize        | Triggered when the browser window is resized.                                                 |
| input         | Fired when the value of an input element changes.                                             |
| contextmenu   | Triggered when the right mouse button is pressed.                                             |
| transitionend | Triggered when a CSS transition ends.                                                         |
| error         | Triggered when an error occurs during loading of an external file.                            |

#### Default Events

- click <a>
    - Automatically changes the URL and goes to that URL.
- submit <form>
    - Refreshes the screen by sending a request to the URL specified in the action attribute of the form.
    - Clears form inputs
    - Changes URL

### Traversing the DOM

|                         |                                                            |
|-------------------------|------------------------------------------------------------|
| element.parentNode      | Returns the parent element of the current element          |
| element.childNodes      | Returns a collection of child nodes of the current element |
| element.firstChild      | Returns the first child element of the current element     |
| element.lastChild       | Returns the last child element of the current element      |
| element.nextSibling     | Returns the next sibling element of the current element    |
| element.previousSibling | Returns the previous sibling element of the current element|
| element.children[index] | Gets the child of the element at the index.                |

## This
The `this` keyword is used to refer to the current object.

- By default the `this` keyword is in the window object.

```
console.log(this) // This will print the window
let planet = {
    name = "Earth",
    printName = () => {
        console.log(this.name)
    },
}
```

## Timing

|                                                    |                                                                                                          |
|----------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| setTimeout(function, milliseconds)                 | The function runs after the delay time in milliseconds. Other code can run while waiting for setTimeout. |
| let interval = setInterval(function, milliseconds) | Runs the function every milliseconds. Other code can run int he background.                              |
| clearInterval(interval)                            | Stops the interval.                                                                                      |

1000 Milliseconds = 1 Second

## +/-/++/-- Operators

```
let variable = 5
let result1 = ++variable // variable becomes 6 and result1 becomes 6
let result2 = --variable // variable becomes 5 and result2 becomes 5
let result3 = variable++ // result3 become 5 and then variable becomes 6
let result4 = variable-- // result4 becomes 6 and then variable becomes 5
```

```
console.log(+"3" + +"5") // 8
    // The +s infront of the string converts it to a num and then those numbers are added together
console.log(-"3" - -"5") // 2
    // The -s infront of the string converrs it to a num, but negates it and then those numbers are subtracted from one another.
console.log(-"-3" + -"5") // -2
```

## Local/Session Storage
Local storage is information stored locally on the browser.

Session storage is information stored locally to that tab.

In incognito/private window it creates a new localStorage and removes it when the window is deleted.

5megabytes max for local storage.

```
localStorage.setItem("key", "value")

localStorage.getItem("key")
    Returns null if nothing is found

localStorage.removeItem("key")

localStorage.clear()
    Removes all local storage foryour site

Never store passwords, even hashed passwords, in the local storage or session storage.
```

## Common APIs

|           |                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------|
| jQuery    | Makes HTML document traversal and manipulation, event handling, animation, and Ajax easier to use. |
| [day.js](https://day.js.org/docs/en/display/format)    | Dates and Calendars                                                                                          |
| bootstrap | Front-end framework.                                                                               |
| jQuery UI | Makes manipulating things easier. Can work with bootstrap. |
| [Axios](https://axios-http.com/docs/intro)     | ajax in jQuery, but without the jQuery. |


### Dayjs

Provides more powerful formatting than the inbuilt Date() in JS

```
var today = dayjs()
today.format("MMM D, YYYY')
today.format('[This is the day: ] ddd')
```

Unix time is the number of seconds from Jan 1st, 1970(epoch time).

## URL of Webpage
Use `document.location` to get properties of the current webpage's URL.

You can get everything after the ? in the URL(query string) by doing `document.location.search`

### Redirect URL
`document.location.href = newURL`

This can be used to go to another one of your pages by setting the new URL to the filepath of an html page.

## Regex
Used to match patterns.

```
function validate(input){
    // Does string start with the word regex
        const pattern = /^(regex).*/gm
    if(input.match(pattern)){
        // Matches the regex
    }else{
        // Doesn't match the regex
    }
}
```