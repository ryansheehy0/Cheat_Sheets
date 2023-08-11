[Home](./README.md)

# Object Oriented Programming(OOP)

Procedural programming is having functions that take in data, manipulate it, then return it.

## Problems with Procedural Programming
- You end up having many different functions all over the place that are hard to group together into folders and files.
- There are a lot of dependencies from one function to another. If you change one function it may brake other functions.
- More complex functions end up having more and more arguments.

## 4 Pillars of OOP

### Encapsulation
Grouping related variables(properties) and functions(methods) that manipulate those variables into a unit called an object.

### Abstraction
Hide the details and complexity behind an interface.

Public and Private properties and methods.

- This reduces the impact of change so if you change a private method or property it doesn't effect anything else on the outside.

### Inheritance
Allows you to eliminate redundant code by reusing classes.

### Polymorphism
Methods can have the same name, but different arguments. This reduces code which would check for certain conditions.

Any children which inherit a class can change how a function work for themselves.

## Dependency Injection

## Static methods
Methods that are associated with the class itself rather than the object of the class. Meaning you can call the static methods directly on the class without needing to create an instance(object) of the class.

## Set and Get methods
A Set and Get method are used when you want to make a variable public, but also want to apply additional logic when that variable is modified or returned.

By default it is recommended to use Set and Get methods incase you want to add additional logic in the future without having to modify your interface thus saving you from re-writing other code.

## Design Patterns
### Decorator
### Singletons
A single object that is shared in your program.

### Factory
- Put all arguments in at once
### Builder Design Pattern
Instead of passing values into the contractor you can use Set methods instead.
  - These Set methods should return the object itself(`this`) to allow for chaining of these setter methods.

This has several advantages:
- It is clear what values you are setting because you call them through a setter
- It cuts down on unnecessary code because you don't need a long list of this.privateVar = argument

### Model View Controller(MVC)
Models folder contains data
Controller is the logic.
The view is getting data to G

### Observer

## Other
- A pure function is one that doesn't have any side effect.
  - Always produces the same output with the same inputs
  - Doesn't use any global variables. Doesn't set or get
- It is good to prevent outside code from being able to interact with functions or variables that it shouldn't. Have private functions and variables.
- There shouldn't be any programming files that have too many lines of code.
  - This means there needs to be more abstraction
- The best functions are ones with no parameters/arguments
- Don't repeat the code you write. No code should be repeated

## Rules for RS endorsed OOP
- Set all properties in classes to private and only use Set and Get methods instead of public properties.
- The only arguments in constructors should be essential to start the object. Any optional argument should be set through Set methods and return `this` to allow for chaining.
  - Programming languages should allow you to change weather a function is private or public to allow for changing interfaces for when optional arguments are set.
- Never use static methods. Either make it an instance method or don't use a class.

Classes are used to create objects from a template.
An object is an unordered collection of related variables and/or functions.

What is schema?