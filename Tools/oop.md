<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# Object Oriented Programming(OOP)

Procedural programming is having functions that take in data, manipulate it, then return it.

The reason to use OOP is to prevent functions from having extremely long arguments and it allows for better organization by group together variables and functions.

## Table of Contents

<!-- TOC -->

- [Object Oriented ProgrammingOOP](#object-oriented-programmingoop)
	- [Table of Contents](#table-of-contents)
	- [Problems with Procedural Programming](#problems-with-procedural-programming)
	- [4 Pillars of OOP](#4-pillars-of-oop)
		- [Encapsulation](#encapsulation)
		- [Abstraction](#abstraction)
		- [Inheritance](#inheritance)
		- [Polymorphism](#polymorphism)
	- [Dependency Injection](#dependency-injection)
	- [Static methods](#static-methods)
	- [Set and Get methods](#set-and-get-methods)
	- [Design Patterns](#design-patterns)
		- [Decorator](#decorator)
		- [Singletons](#singletons)
		- [Factory](#factory)
		- [Builder Design Pattern](#builder-design-pattern)
		- [Model View ControllerMVC](#model-view-controllermvc)
		- [Observer](#observer)
	- [Other](#other)
	- [Use Builder pattern](#use-builder-pattern)

<!-- /TOC -->

## [Problems with Procedural Programming](#table-of-contents)
- You end up having many different functions all over the place that are hard to group together into folders and files.
- There are a lot of dependencies from one function to another. If you change one function it may brake other functions.
- More complex functions end up having more and more arguments.

## [4 Pillars of OOP](#table-of-contents)

### [Encapsulation](#table-of-contents)
Grouping related variables(properties) and functions(methods) that manipulate those variables into a unit called an object.

### [Abstraction](#table-of-contents)
Hide the details and complexity behind an interface.

Public and Private properties and methods.

- This reduces the impact of change so if you change a private method or property it doesn't effect anything else on the outside.

### [Inheritance](#table-of-contents)
Allows you to eliminate redundant code by reusing classes.

### [Polymorphism](#table-of-contents)
Methods can have the same name, but different arguments. This reduces code which would check for certain conditions.

Any children which inherit a class can change how a function work for themselves.

## [Dependency Injection](#table-of-contents)

## [Static methods](#table-of-contents)
Methods that are associated with the class itself rather than the object of the class. Meaning you can call the static methods directly on the class without needing to create an instance(object) of the class.

## [Set and Get methods](#table-of-contents)
A Set and Get method are used when you want to make a variable public, but also want to apply additional logic when that variable is modified or returned.

By default it is recommended to use Set and Get methods incase you want to add additional logic in the future without having to modify your interface thus saving you from re-writing other code.

## [Design Patterns](#table-of-contents)
### [Decorator](#table-of-contents)
### [Singletons](#table-of-contents)
A single object that is shared in your program.

### [Factory](#table-of-contents)
- Put all arguments in at once
### [Builder Design Pattern](#table-of-contents)
Instead of passing values into the contractor you can use Set methods instead.
  - These Set methods should return the object itself(`this`) to allow for chaining of these setter methods.

This has several advantages:
- It is clear what values you are setting because you call them through a setter
- It cuts down on unnecessary code because you don't need a long list of this.privateVar = argument

### [Model View Controller(MVC)](#table-of-contents)
Models folder contains data
Controller is the logic.
The view is getting data to G

### [Observer](#table-of-contents)

## [Other](#table-of-contents)
- A pure function is one that doesn't have any side effect.
  - Always produces the same output with the same inputs
  - Doesn't use any global variables. Doesn't set or get
- It is good to prevent outside code from being able to interact with functions or variables that it shouldn't. Have private functions and variables.
- There shouldn't be any programming files that have too many lines of code.
  - This means there needs to be more abstraction
- The best functions are ones with no parameters/arguments
- Don't repeat the code you write. No code should be repeated

Classes are used to create objects from a template.
An object is an unordered collection of related variables and/or functions.

## [Use Builder pattern](#table-of-contents)
```javascript
function Class({arg1, arg2}, {optionalArg1} = {}) {

  this.setOptionalArg1(arg){
    optionalArg1 = arg
    return this
  }

  this.optionalFunction = function(){
    if(typeof optionalArg1 === "undefined"){
      throw new Error("optionalFunction needs optionalArg1")
    }
    // Run code that uses optional arguments
  }
}
```