[Home](../README.md)

# C++
My personal notes on C++.

<!-- TOC -->

- [To Do](#to-do)
- [main](#main)
- [Data Types](#data-types)
	- [Int based data types](#int-based-data-types)
	- [Float based data types](#float-based-data-types)
	- [Data type notes](#data-type-notes)
		- [Truthy and Falsy](#truthy-and-falsy)
		- [Multiple variables on one line](#multiple-variables-on-one-line)
		- [Variable names/Identifiers](#variable-namesidentifiers)
		- [Assigning values](#assigning-values)
		- [Int vs Float Division](#int-vs-float-division)
		- [Dividing by zero](#dividing-by-zero)
		- [Int vs Float Modulus](#int-vs-float-modulus)
		- [post-fix vs pre-fix increment](#post-fix-vs-pre-fix-increment)
	- [Const](#const)
	- [Auto](#auto)
- [Headers](#headers)
- [Namespaces](#namespaces)
- [Character escapes](#character-escapes)
- [Pointers and references](#pointers-and-references)
	- [Function pointers](#function-pointers)
	- [Arrays](#arrays)
		- [Two dimensional arrays](#two-dimensional-arrays)
- [Order of operations](#order-of-operations)
- [Loops and Conditions](#loops-and-conditions)
	- [Switch](#switch)
	- [Do While loops](#do-while-loops)
	- [Single line conditions](#single-line-conditions)
	- [Range based for loop](#range-based-for-loop)
- [Functions](#functions)
	- [Types of functions](#types-of-functions)
	- [Pass by value or reference](#pass-by-value-or-reference)
	- [Optional arguments](#optional-arguments)
	- [Function overloading](#function-overloading)
	- [Lambda functions](#lambda-functions)
- [Global and static variables](#global-and-static-variables)
- [Exception/Error handling](#exceptionerror-handling)
- [Templates](#templates)
- [new and delete](#new-and-delete)
- [Enums](#enums)
- [Structs](#structs)
- [Classes](#classes)
	- [Constructors and Destructors](#constructors-and-destructors)
	- [Operator overloading](#operator-overloading)
	- [Inheritance](#inheritance)
		- [Virtual and Override](#virtual-and-override)
		- [Composition vs Inheritance](#composition-vs-inheritance)
	- [Using heap memory in classes](#using-heap-memory-in-classes)
- [Classes](#classes)
	- [Constructors and destructors](#constructors-and-destructors)
	- [Operator overloading](#operator-overloading)
	- [Inheritance](#inheritance)
		- [Composition over Inheritance](#composition-over-inheritance)
	- [Copy constructor and overloading the = operator](#copy-constructor-and-overloading-the--operator)
	- [The rule of 3](#the-rule-of-3)

<!-- /TOC -->

## To Do
- cassert for testing
- openssl
- casting
- How the linker works
	- dynamic vs static linking
- Variadic functions
- thrown error types
- typedef
- friend and operator keywords?
- Singletons
- Regex in C++
- typeid
- Multi-threading
- Modules?
	- `import` how does this effect header files
- left hand side(lhs) means that it can be assigned to. Can be placed ont he left hand side of the assignment(=) operator.
- right hand side(rhs) means that it cannot be assigned. Can only be placed on the right hand side of the assignment(=) operator, like a constant.

## [main](#c)
The main function is the entry point of a program.
- function signature
	- `int main()` - Doesn't take in command line arguments.
	- `int main(int argc, char *argv[])` - Allows command line arguments.
		- `argc` is the number of arguments
		- `argv` is an array of strings for the arguments. This includes the program name.
- Return type
	- `return 0;` - return without any errors
	- `return 1;` - return with an error

## [Data Types](#c)
The smallest memory unit is 1 byte(8 bits).

### [Int based data types](#c)

| Name      | Bytes  | Notes                                        |
|-----------|--------|----------------------------------------------|
| bool      | 1      | Can use `true` or `false` keywords           |
| char      | 1      | Uses `''`s                                   |
| wchar_t   | 2 or 4 | Larger char encoding standards like unicode. |
| short     | 2      | Same as `short int`                          |
| int       | 2 or 4 | Bytes depends on the platform                |
| long long | 8      | Same as `long long int`                      |

- When you want the size to be clearly defined
	- int8_t, int16_t, int32_t, int64_t
	- uint8_t, uint16_t, uint32_t, uint64_t
- `""`s return a `const char*` array that has a null terminating character.

### [Float based data types](#c)

| Name        | Bytes |
|-------------|-------|
| float       | 4     |
| double      | 8     |
| long double | 12    |

### [Data type notes](#c)

#### [Truthy and Falsy](#c)
- Anything positive or negative is truthy and `0` is falsy.
- `(x = #)` returns `x` not `#`
	- Ex: `x = 10` returns `10`
	- Ex: `x = 0` returns `0`
	- Ex: `int32_t x = 2'147'483'648` returns `-2147483648`

#### [Multiple variables on one line](#c)
- Declaring multiple variables on one line
	- `int x, y;`
- Setting multiple variables on one line
	- `int x = 10, y = 20;`
- Assigning multiple variables on one line
	- `x = y = 20;`
	- `x` and `y` will both be equal to `20`
- Command equals multiple variables
	- `x += x + 3;` is the same as `x = x + x + 3;`

#### [Variable names/Identifiers](#c)
- Variable names can only use letters, underscores, and digits, and cannot start with digits.
	- Ex: `_this_is_a_valid_variable_name`
- Variable names are case sensitive

#### [Assigning values](#c)
- You can use `'` to separate very long numbers.
	- Ex: `1'999'999`
- You can assign floats using scientific notation.
	- `6.08e2` = `6.08 x 10^2` = `608`
	- `6.08e-2` = `0.0608`
- It is recommended to start floats with `0` instead of a `.`

#### [Int vs Float Division](#c)
- Integer division is truncated
- In order to get float division, either the numerator or denominator has to be a float/double.
	- `1/2` will return `0`
	- `1.0/2` will return `0.5`
	- `1/2.0` will return `0.5`
	- `1.0/2.0` will return `0.5`

#### [Dividing by zero](#c)
- Dividing by zero in integer division gives a runtime error
- Float division
	- `0.0/0.0` outputs not a number(nan)
	- `1.0/0.0` outputs inf
	- `-1.0/0.0` outputs -inf

#### [Int vs Float Modulus](#c)
- Compiler error if you use modulus with floats/doubles.
- Modulus can only work with int data types

#### [post-fix vs pre-fix increment](#c)
- `x++` returns `x` then increments it by 1
- `++x` increments `x` then returns `x`

### [Const](#c)
- By convention use SCREAMING_CASE
- By convention declare before any other variables
- Use `const` over `#define`
	- Modern compilers do the same thing as `#define`
	- `const` has type checking and syntax checking
	- `const` is known to debuggers
	- `const` can be scoped to the block
- A function returning a `const` means that the returned value cannot be modified, but this only really applies to references or pointers.

### [Auto](#c)
`auto` tells the compiler to determine the variable's type by the initial value given.
- Ex: `auto x = "apple";` gets assigned const char*
- Ex: `auto x = 0.01;` gets assigned double
- Ex: `auto x` gives an error

## [Headers](#c)
The purpose of header files is to allow you to separate the declaration(.h) and the definitions(.cpp). The declarations(.h) can be shared across multiple files. This has a couple of benefits:
- It separates the interface(.h) and the implementation(.cpp), so that when using the code you just have to worry about what you can use.
- If you only change the implementation(.cpp) and not the interface(.h), then the compiler only has to re-compile that implementation(.cpp) and not other implementations(.cpp).
- If you only change the .cpp file and not the .h file, then the compiler only has to re-compile the .cpp file and not the other .cpp files. Because the interface(.h) didn't change, only the implementation(.cpp).

```C++
// .h
#pragma once

class Class {
	private:
		int _x = 0;
	public:
		void print();
};
```

```C++
// .cpp
#include "Class.h"
#include <iostream>

Class::print() {
	std::cout << _x << "\n";
}
```

- Prevent multiple header file inclusions to prevent multiple declarations.
	- `#pragma once` - This is newer and is recommended
	- Or you can use header guards
	```C++
	#ifndef __CLASS_NAME_H__
	#define __CLASS_NAME_H__
	// Header file
	#endif
	```

## [Namespaces](#c)
Namespaces define a region/scope used to prevent naming conflicts

```C++
namespace namespaceName {
	int x;
}

namespaceName::x = 10;
```

- You can have namespaces automatically used with `using namespace namespaceName`.
	- This isn't recommended because it can result in naming conflicts.
- You can use `{}` to define a new scope.

## [Character escapes](#c)

| Character | Description                       |
|-----------|-----------------------------------|
| `\'`      |                                   |
| `\"`      |                                   |
| `\\`      | backslash                         |
| `\a`      | audible bell                      |
| `\b`      | backspace                         |
| `\f`      | form feed - new page              |
| `\n`      | new line                          |
| `\r`      | carriage return                   |
| `\t`      | horizontal tab                    |
| `\v`      | vertical tab                      |
| `\o##`    | octal output                      |
| `\x##`    | hexadecimal output                |
| `\u####`  | prints unicode. Only works on g++ |
| `\Nname`  | unicode character from name       |
| `\0`      | Null                              |

## [Pointers and references](#c)

| Code                    | Description                                                         |
|-------------------------|---------------------------------------------------------------------|
| `int* ptr;`             | Creates a pointer pointing to an int. Enough memory for an address. |
| `*ptr`                  | Dereferences the ptr                                                |
| `int& x = y;`           | `x` is a reference to `y`. `x` and `y` always have the same value.  |
| `&ptr`                  | Gets address of ptr.                                                |
| `ptr`                   | Gets the value in ptr. The address it points to.                    |
| `ptr->`                 | Is the same as `(*ptr).`                                            |
| `const int* xPtr = &x;` | Pointer to a const int. Can't change the dereference.               |
| `int* const xPtr = &x;` | Pointer to an int, but the pointer cannot change.                   |

### [Function pointers](#c)

```C++
void (*func)(int, int);
```

You can also use `#include <functional>` and `function<void(int, int)> func;`

### [Arrays](#c)
Arrays in C++ store a sequences of variables in contiguous memory. The array is a pointer to the first element of the array. Accessing an element with `arr[index]` is equivalent to dereferencing the pointer at the memory location `*(arrPtr + index)`.
- Define with random data
	- Ex: `int arr[3];`
- Initialize with zeros
	- Ex: `int arr[3] = {1};` initializes with 1, 0, 0
	- Ex 2: `int arr[3] = {};` initializes with 0, 0, 0
- You don't have to specify the size
	- Ex: `int arr[] = {0, 0, 0};` the size is 3

#### [Two dimensional arrays](#c)
Since arrays are stored in continuous memory, a two dimensional array(or more dimensions) can also be reprehended with a one dimensional array.
- `int twoDArr[row][col]` or `int oneDArr[row * col]` - Creates a 2d array.
- `arr[row][col]` or `arr[(cols * row) + col]` - Access an element in the 2d array.

Each of these array may contain the same memory, but their data types are different.
- `int twoDArr[row][col]` type is `int *[col]`
- `int oneDArr[row * col]` type is `int *`

## [Order of operations](#c)
Operations with the same precedence are executed according to their associativity, left to right or right to left.

| Precedence | Operation                    | Associativity |
|------------|------------------------------|---------------|
| 1          | :: - scope                   | Left to right |
| 2          | x++, x--                     | Left to right |
|            | type() - functional case     |               |
|            | func(), arr[]                |               |
|            | ., ->                        |               |
| 3          | ++x, --x                     | Right to left |
|            | +x, -x, !, ~                 |               |
|            | (type) - C-style case        |               |
|            | *ptr, &var, sizeof           |               |
|            | new, new[], delete, delete[] |               |
| 4          | .*, ->*                      | Left to right |
| 5          | x*y, x/y, x%y                | Left to right |
| 6          | x+y, x-y                     | Left to right |
| 7          | <<, >>                       | Left to right |
| 8          | <, <=, >, >=                 | Left to right |
| 9          | ==, !=                       | Left to right |
| 10         | &                            | Left to right |
| 11         | ^                            | Left to right |
| 12         | \|                           | Left to right |
| 13         | &&                           | Left to right |
| 14         | \|\|                         | Left to right |
| 15         | x?y:z, throw, =              | Right to left |
|            | +=, -=, *=, /=, %=, <<=, >>= |               |
|            | &=, ^=, \|=                  |               |
| 16         | ,                            | Left to right |

## [Loops and Conditions](#c)

### [Switch](#c)
- Cannot be used with strings or floats.

```c++
switch (x) {
	case 0:
		break;
	case 1:
	case 2:
		// 1 or 2
		break;
	default:
		break;
}
```

### [Do While loops](#c)

```c++
do {
} while (true);
```

### [Single line conditions](#c)

```c++
if (true) cout << "true" << endl;

if (true)
	cout << "true" << endl;
else
	cout << "false" << endl;

for (int i = 0; i < 10; i++)
	cout << i << endl;

while (true)
  cout << "infinity ";
```

### [Range based for loop](#c)
- The list has to have an iterator in order to work.

```c++
std::vector<int> arr = {1, 2, 3, 4};

for (int num : arr) {
}
// This is the same as
for (std::vector<int>::iterator it = arr.begin(); it != arr.end(); it++) {
	int num = *it;
}
```

- If const is used as the data type then `::const_iterator` is used instead.

## [Functions](#c)
- Functions cannot be declared within other functions.

| Term           | Example              |
|----------------|----------------------|
| prototype      | `void func(int);`    |
| header         | `void func(int arg)` |
| implementation | `{ /* body */ }`       |

- The purpose of putting a function's prototype at the top is to allow the function to be used before it is implemented.

### [Types of functions](#c)

|                          |                                                                             |
|--------------------------|-----------------------------------------------------------------------------|
| `constexpr void func();` | A function can be evaluated at compile time if possible.                    |
| `inline void func();`    | Compiler searches and replaces. Speed up performance, but uses more memory. |

### [Pass by value or reference](#c)
- If you don't want to change the argument
	- If the argument is less than 64bits/8bytes
		- Pass by value `void func(int x)`
	- Else
		- Pass by const reference - `void func(const Class& x)`
- If you do want to change the argument
	- Pass by pointer - `void func(Class* x)`

Following these rules makes it clear that an object is being modified by a function because you have to specify the address when passing it as an argument.
- For an array you want to change use `int (*arr)[]`
- For an array you don't want to change use `const int arr[]`

### [Optional arguments](#c)
- Any argument after an optional argument must also be an optional argument.

```c++
int test(int a, int b = 4, int c = 10){}

test(1, 2, 3);
test(1, 2);
test(1);
```

- If you have a function prototype, you can only put the default values in the prototype and not the function header.

### [Function overloading](#c)
- Function overloading are multiple functions with the same name, but different argument types.
	- The compiler determines which function to call based on the argument types.
- Functions that return different types don't overload.

### [Lambda functions](#c)
Lambda functions allow you to easily pass small functions into another function. They take the form of `[capture list](arguments){function body}`. You can also specify a return type with `[]() -> type {}`
- The capture list specifies what variables are accessible from the outside scope.
	- You can use `[&]` to have access to all the variables in the outside scope as pass by reference.
	- You can use `[=]` to have access to all the variables in the outside scope as pass by value.

## [Global and static variables](#c)
- Static variable have their memory persist across function calls. They are scoped to the function they are defined in.
- Global variables are defined outside any function and can be used by any function.
	- They are automatically set to 0 if not given a value.
	- Usually global variables are constants in order to prevent these side effects.

## [Exception/Error handling](#c)
- If you want to exit your program from anywhere you can do `exit(1);`
- The purpose of throwing errors
	- When the return type doesn't support errors.
		- Ex: For the func `int add(int x, int y)` you can't return -1 as an error because it could be a legitimate value.
	- When you need to bubble up errors through many functions.
		- You don't have to check for an error and return it. You can just call the function.

```C++
void func1() {
	throw "String error";
}

void func2() {
	func1();
}

void func3() {
	try {
		func2();
	} catch (const char* error) {
		// handle error
	}
}
```

- `catch (...)` allows you to catch all errors regardless of their type
- `throw;` allows you to throw the previously thrown error
- There is a hierarchy of C++ errors.
	- std::exception
		- std::bad_alloc - When memory allocation fails
		- std::bad_cast - When failing to dynamically cast using `dynamic_cast`
		- etc.
		- std::logic_error
			- std::domain_error - When a function receives an arg outside its domain.(Like `sqrt` receiving a negative num.)
			- std::invalid_argument - When the arguments to a function are invalid
			- std::length_error - When an operation exceeds the allocated size
			- std::out_of_range - When trying to access an element outside the valid range.
		- std::runtime_error
			- std::range_error - When a computation results in a value outside the valid range. Function expects to return in a certain range, but the computation is outside of that range.
			- std::overflow_error - When an arithmetic operation results in an overflow.
			- std::underflow_error - When an arithmetic operation results in an underflow.
			- std::ios_base::failure - When the input/output operations fail. Common if a file can't read or write.

## [Templates](#c)
Templates are used to allow the same piece of code to use different data types.

```C++
template <typename T>
void print(T value) {
	std::cout << value << "\n";
}

print(5) // Defined implicitly based upon the type of the argument
print<char>('a') // Defined explicitly
```

- Using `class` is the same as using `typename`

## [new and delete](#c)
Heap memory is used when teh size is only known at run time.
- `new` allocates memory on the heap and returns its address.
- `delete` frees the allocated memory.
	- Deleting a nullptr does nothing.

```C++
int* ptr = new int;
delete ptr;
// With arrays
int* arr = new int[10];
delete[] arr;
```

## [Enums](#c)
Enums define a variable's allowed values by restricting it to a predefined set of named constants, improving code clarity and reducing invalid inputs.
- Enums automatically count up from 0, but they can be changed by assigning them.
	- Ex: `enum Num {ONE = 1, TWO, THREE}`

```C++
enum Shape {CIRCLE, SQUARE, TRIANGLE};
enum class Color {RED, GREEN, BLUE};

Shape s = CIRCLE;
Color c = Color::RED;
```

- The values in regular enums are treated as ints, by default, but the values in enum classes are treated as their own types.
	- Ex: `CIRCLE == 0` is true while `Color::RED == 0` is false.
- You can change the default enum type by doing `enum Color : char {RED, GREEN, BLUE};`

## [Structs](#c)
The only difference between structs and classes is that by default structs' members are public. However, the convention is to only use Structs to group variables together.
- Use the member access operator `.` to get each element in the struct.

```C++
struct Point {
	int x;
	int y = 10; // Default value
};

Point pt = {10, 20};
	// Or
Point pt;
pt.x = 10;
pt.y = 20;
	// Or
Point pt = {.x=10, .y=20};
```

## [Classes](#c)
- `const` after methods
- Definitions vs Declarations

### [Constructors and Destructors](#c)
- Constructor initializer list `:`

### [Operator overloading](#c)

### [Inheritance](#c)

#### [Virtual and Override](#c)

#### [Composition vs Inheritance](#c)
- Contains(has-a) relationship vs Belongs to(is-a) relationship.
	- Ex: A car has a engine so you should use composition.
	- Ex: A truck is a car so you should use inheritance.

### [Using heap memory in classes](#c)
- The rule of 3
	- Destructor
		- How delete interacts with the destructor.
	- Copy constructor
	- Overload the assignment operator
- Explain copying pointers vs copying the underlying data. That's why you need copy constructor and overload the assignment operator.



## [Classes](#c)

- `const` after a method says that it doesn't modify any member variables.
	- Ex: `void method() const`
	- These methods are allowed to be called by constant objects.
- Definitions vs Declarations

```C++
// Definitions
class Class {
	private:
	public:
}
```


```C++
class Class {
};
```

- When you want to modify an object as a parameter passing by pointer is preferred over a pass by reference.
- A very common pattern is to have one class that represents a unit, and another class which has a vector of units. This allows methods to be built that apply to one component and then to all components.

- If a class doesn't define a constructor, then it's given a default constructor.
- Once a class defines a constructor, then the default constructor isn't automatically created.

- Construcotr initializer list `:`
	- Uses values to initalize any objects instead of creting it and then setting it.
	- Used to call inherited parent's constructor.
		- You can't access the parent's protected member variables with this syntax.

- `this` is a pointer to the current object.
	- Used to differentiate between a local variable and a member variable. To get the member variable: `this->memberVar`

- When an object is pass by reference or pointer, then the destructor is not automatically called.

- static member variables are not attached to the object, but the class itself.
- static member functions can only access other static member variables/functions.

- The demonstrator should delete any heap memory that was created in the class.

- Methods can return `*this` in order to chain methods together
```c++
MyClass& setY(int y) {
	_y = y;
	return *this;
}

MyClass& setX(int x) {
	_x = x;
	return *this;
}

myObj.setY(10).setX(20);
```

- The default constructor goes away when you have one contractor with arguments. If you still want it, then use `Class() = default;`

### [Constructors and destructors](#c)

- The destructor is not called automatically when creating an object with the `new` keyword.
	- The `delete` keyword calls the destructor and then deallocates the memory.

### [Operator overloading](#c)
- member function named `operator+`
	- Only requires the right hand side(rhs) as the parameter because the left is implied to be the object itself.

```C++
class Time {
	public:
		Time operator+(Time rhs);
		Time operator+(int rhs); // This only works if the right hand side is an int. If the left hand side is an int, then it doesn't work.
}
```

- Overloading conditionals

```C++
class Time {
	public:
		bool operator==(const Time& lhs, const Time& rhs);
		bool operator<(const Time& lhs, const Time& rhs);
}
```

- It's common to thoroughly write out the == and < operators and define the other conditional operators off of those two.
	- `bool operator!=(const Time& lhs, const Time& rhs) { return !(lhs == rhs); }`
	- `bool operator>(const Time& lhs, const Time& rhs)  { return rhs < lhs; }`
	- `bool operator<=(const Time& lhs, const Time& rhs) { return !(lhs > rhs); }`
	- `bool operator>=(const Time& lhs, const Time& rhs) { return !(lhs < rhs); }`

### [Inheritance](#c)
- abstract class - Guides the design of subclasses, but cannot be instantiated as an object. Same as interfaces.
	- Any class with one or more pure virtual functions is abstract.
	- pure virtual function - Virtual function that provides no definition and thus requires all derived classes to override it.
		- Ex: `virtual void print() const = 0;`
		- Abstract classes don't need to override pure virtual functions. As long as the pure virtual method is eventually overridden by a concrete (non-abstract) class, it will work.
- concrete class - Not an abstract class.
- derived class/subclass - A class which inherits another class so that you don't have to duplicate code.
	- `class Derived : public Base{};`
		- public: - public members of base class are accessible as public members of derived class and protected members of base class are accessible as protected members of derived class.
			- public = public and protected = protected
		- protected: - public = protected and protected = protected
		- private: - public = private and protected = private
		- This allows a derived class to control the access level of its inherited base class's member variables, which is especially important if the derived class is further inherited by another class.
		- Derived classes cannot use `:`s in their constructor to set their super/base class's member variables.
- base class/superclass - A class which gets inherited from.
- protected: - The derived class can access it, but it's private to any instances of the base class.
- overriding - Derived class has the exact same function signature.
	- To call the original method in the overrided method you can do `Base::method`.
- overloading - Function has different argument types.
	- If a derived class overloads a base class's public method, then you cannot call that public method from an instance of the derived class. It has to be the exact method that was overloaded.

```C++
class Base {
	public:
		void show(int x) {
			std::cout << "show(int): " << x << std::endl;
		}
};

class Derived : public Base {
	public:
		void show(double y) {
			std::cout << "show(double): " << y << std::endl;
		}
};

int main() {
	Derived d;
	d.show(3.14);
	d.show(10); // Error because of overloading
	d.Base::show(10);  // Calls the base class's show explicitly
}
```

- Polymorphism - Same name, but a different meaning. Using a derived classes as base classes, but overriding different methods.
	- Compile time polymorphism
		- Function overloading
	- Runtime polymorphism
		- When you call a method on a base class variable. It could either be the base class or the derived class, which is determined at runtime.
		- Only works if you use virtual and override keywords.
		- virtual function - member function that may be overridden in a derived class and is used for runtime polymorphism.
			- The compiler creates a virtual table
			- If virtual isn't used, then the default method is used based upon what type the compile thinks the object is(the base class).
		- override - An optional keyword used to indicate that a virtual function is overridden in a derived class.
			- Ex: `void print() const override {}`
			- The override keyword is recommended because ti produces a compiler error if virtual is left out from the base class's member function.

- A vector of heap pointers

#### [Composition over Inheritance](#c)
Consider a program that catalogs the types of trees in a forest. Each tree object contains the tree's species type, age, location, and estimated size based on age. Each species uses a different formula to estimate size based on age. This program will benefit from an abstract class.
- Inheritance: Tree class as the parent class. Child classes for each different species of tree.
- Composition: Tree class which takes in an abstract class/interface of TreeSizeCalculator. You then have to create separate tree size calculator classes for each species.

Composition - One object maybe made up of other object

Is there a useful purpose for inheritance?
- Pear "is a" Fruit - Inheritance
- House "has a" door - Composition

### [Copy constructor and overloading the = operator](#c)
- When you do a pass by value argument for an object that has a pointer member variable, that pointer value is copied to the argument. When this argument goes out of scope, its destructor is called. This destructor can free the pointer memory. This is a problem when the original object, that was passed into the argument, tries to use this pointer again.
- To solve this problem, you use a copy constructor.
	- Copy constructor - A constructor that is automatically called when an object of the class is passed by value to a function or when an object is initialized by copying another object.
	- The copy constructor makes a deep copy, creating new heap variables.
		- Ex: `void print(obj);`
		- Ex: `MyClass obj2 = obj1;`

```C++
class MyClass {
	public:
		MyClass() {
			num = new int;
		}

		MyClass(const MyClass& obj) {
			num = new int;
			*num = *(obj.num);
		}

		~MyClass() {
			delete num;
		}

	private:
		int* num;
};
```

- When you assign an object to another object and it's already initialized, in order to do a deep copy, you need to overload the = operator.
	Ex: `obj2 = obj1`

```C++
MyClass& MyClass::operator=(const MyClass& rhs) {
	if (this != &rhs) { // Don't self assign
		delete num; // Free old memory
		num = new int; // Create new memory
		*num = *(rhs.num); // Assign new memory
	}
	return *this;
}
```

### [The rule of 3](#c)
- Any class that uses heap memory should define these 3 member functions.
	- Destructor
	- Copy constructor
	- Overloading the = operator
