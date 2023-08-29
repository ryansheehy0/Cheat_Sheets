[Home](./README.md)

# Advanced Programming Tips

## General
- Use guard clauses in functions when possible

```javascript
function test(arg) {
  if(arg === null) return

}
```

- Use descriptive variable/function names

- Put variables in order if you can

```javascript
let test          = 0
let test1         = 1
let variable_name = 2
```

- Set all properties/variables in classes to private and only use setter and getter methods instead of public properties.
  - You want to keep your class's interface consistent and if you want to add additional functionality when a variable is set or gotten then you have to make it a function and thus
  - The only exception to this is if the language you are using allows for set and get methods that are called by calling the variable regularly. Like `get` and `set` in classes in JS.

- Make all set functions return `this` to allow for chaining.

- The only 2 types of classes are regular classes and singletons.
  - Never use static methods

- If a class has a lot of methods then organize those methods into other classes and create an object in your main class that is then used to call those methods.
  - The folder should be named after the main class and should contain the files for the main class and all other children classes.

- Never have too many folders or subfunction in one place.
  - This means that it isn't organized
  - It is recommended to use the MVC model
    - Model is responsible for all the data logic
    - View is responsible for making a presentation of the data
    - Controller is responsible for Take user input -> Give input to model -> Get data from model -> Give data to view -> Get presentation from view -> Give presentation to user.

- Try to never reuse code.
  - If 2 sets of functions using the same code, then create a separate function.

- Try to never keep changing the same variable for too long.
  - This will make your code hard to follow along

## Javascript
- Keep in mind arguments being `undefined` or `null`
- Use Class Constructor Functions instead of the `class` keyword
  - Don't need a separate constructor function
  - Easy to make private variables
  - Don't have to use the `this` keyword when using variables
- Optional arguments into functions should have defaults and be put into objects
- Don't use ;s
- Use a space inbetween the ()  for functions
- For functions use `() {` instead of `(){}`
- Use regular functions when using separate functions
- Use arrow functions when having functions as arguments

```javascript
function test(arg1, {optional1 = 1, optional2 = 2} = {}) {
}
```