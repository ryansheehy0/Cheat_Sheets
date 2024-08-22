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

# C++

My personal notes on C++.

<!-- TOC -->

- [Things to research](#things-to-research)
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
	- [Casting](#casting)
	- [Auto](#auto)
- [Headers](#headers)
- [Namespaces and using](#namespaces-and-using)
- [Character escapes](#character-escapes)
- [Pointers and references](#pointers-and-references)
	- [Function pointers](#function-pointers)
	- [Constants with pointers](#constants-with-pointers)
	- [Arrays](#arrays)
- [Order of operations](#order-of-operations)
- [Loops and Conditions](#loops-and-conditions)
	- [Switch](#switch)
	- [Do While loops](#do-while-loops)
	- [Single line conditions](#single-line-conditions)
	- [Range based for loop](#range-based-for-loop)
- [Functions](#functions)
	- [Types of functions](#types-of-functions)
	- [Reference arguments](#reference-arguments)
	- [Optional arguments](#optional-arguments)
	- [Function overloading](#function-overloading)
- [Custom Scope](#custom-scope)
- [Global and static variables](#global-and-static-variables)
- [Exception/Error handling](#exceptionerror-handling)

<!-- /TOC -->

## Things to research
- Header files
- Error/Exception handling
- typedef
- friend and operator keywords?
- Operator overloading
- Singletons
- Regex in C++
- Casting
	- `const_cast`, `static_cast`, `reinterpret_cast`, `dynamic_cast`
	- Why not use C style casting
- typeid
- `new` and `delete`
- Dereferencing pointers with `->`
- Templates
	- `template<class T> class Stack`
	- `template<class T> void Stack<T>::push(T c)`
	- Do templates always have to have class in them? Why?
	- How to do size for a template?
	- Done at compile time?
- `virtual` keyword for functions?
	- Virtual means it maybe defined later in a class derived from this one.
	- `= 0` says that it has to be implemented by a child class
	- Can be used to create an interface
	- Has to determine which function to use at runtime. Uses a virtual function table to do this.
- Deconstructors
	- Destructor is called when an object goes out of scope
- Inheritance
	- `:public `
- Interfaces
- string functions
- array functions
- Classes
	- You can also define methods outside of classes with `void Class::func() {/*Define func*/}`
	- Are classes essentially their own namespace? Is that why enum class works?
- `typeid`
- type fields? An instance of an enum?
	- A variable that can only have the types specified in the enum.
- Multi-threading
- Modules?
	- `import` how does this effect header files
- Debugging c++ in vs code
	- Multiple files
	- Multiple 

- `"a"` outputs a null terminated array of characters, while `'a'` is just that character.
	- `"a"` is the same as `['a', '\0']`

## [main](#c)
`int main()` is the start of the program.

- `int main(int argc, char *argv[]){}`
	- `int argc` is the number of arguments passed to the program via the terminal, including the program name.
	- `char **argv` is an array of strings of the arguments separated by spaces, including the program name.
- `return 0;` tells the program that main returned without any errors.
- `return 1;` tells the program that main returned with an error.

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
	- Ex: `x = 2'147'483'648` returns `-2147483648`

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
- Ex: `1/2` will return `0`
- Ex: `1.0/2` will return `0.5`
- Ex: `1/2.0` will return `0.5`
- Ex: `1.0/2.0` will return `0.5`

#### [Dividing by zero](#c)
- Dividing by zero in integer division gives a compiler error
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
- By convention use snake case with all capital letters
- By convention declare before any other variables
- Use `const` over `#define`
	- Modern compilers do the same thing as `#define`
	- `const` has type checking and syntax checking
	- `const` is known to debuggers
	- `const` can be scoped to the block

### [Casting](#c)
- Casting is done at compiler time so it's up to the programmer to make sure they are casting correctly
- `static_cast<data type>(variable)`
- When a float gets cast to an int the decimal is truncated. `1.9 -> 1`

### [Auto](#c)
`auto` tells the compiler to determine the variable's type by the initial value given.
- Ex: `auto x = "apple";` gets assigned const char*
- Ex: `auto x = 0.01;` gets assigned double
- Ex: `auto x` gives an error

## [Headers](#c)
Why header files?
- Allows for separate code compilation
- 

Header fil
When you use a function that isn't defined in your code you get 2 errors.

First, a compile time error because the function isn't declared.
- The compiler generates .o files which may have dependencies to other functions defined in libraries.

Second, a link time error because the linker cannot find the function.
- The linker takes the .o files and combines then and tries to find any unmet dependencies.
- When linking you have to specify the dynamic linked file or the static linked file.
	- Dynamic links are needed elsewhere on the computer and when the executable is ran they are gotten.(.so files)
	- Static links are built into the executable and aren't needed elsewhere on the computer, however they increase the size of your executable.

Header files
- allow any functions to be declared for compile time.
- specifies an interface for using a .cpp file.

## [Namespaces and using](#c)

```C++
namespace namespaceName {
	// Group 
}
```

What are namespaces and what are they used for?

`using namespace std;`

- To access a namespace use the `namespace::command`.

- You can define a function outside of the namespace itself.

```C++
namespace Namespace {
	void func1() {/*Define func1*/}
}
// You can also do
void Namespace::func2() {/*Define func2*/}
```

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

|               |                                         |
|---------------|-----------------------------------------|
| `int* ptr;`   | Contains enough memory to store address |
| `&ptr`        | Gets address of pointer                 |
| `ptr`         | Gets the value in ptr                   |
| `*ptr`        | Dereferences ptr                        |
| `int& x = y;` | When `x` is assigned `y` also changes   |

### [Function pointers](#c)
`void (*name)(int, int) = function;`

### [Constants with pointers](#c)
- A pointer to a constant
- A constant pointer to a data

### [Arrays](#c)
Arrays in C++ store a sequences of variables in contiguous memory. The array name is a pointer to the first element of the array.Accessing an element with `arr[index]` is equivalent to dereferencing the pointer at the memory location `*(arrPtr + index)`.

- Define with random data
	- Ex: `int arr[3];`
- Initialize with zeros
	- Ex: `int arr[3] = {1};` initializes with 1, 0, 0
- You don't have to specify the size
	- Ex: `int arr[] = {0, 0, 0};` the size is 3
- Constants with array
	- Ex: `const int arr[3]` means that it's an array of constant ints.

## [Order of operations](#c)

| Order | Operation              |
|-------|------------------------|
| 1     | ()                     |
| 2     | `::`                   |
| 3     | x++ x-- function calls |
| 4     | ++x --x +x -x !        |
| 5     | * / %                  |
| 6     | + -                    |
| 7     | << >>                  |
| 8     | < <= > >=              |
| 9     | == !=                  |
| 10    | &&                     |
| 11    | \|\|                   |
| 12    | a?b:c = += -=, etc     |

## [Loops and Conditions](#c)

### [Switch](#c)
- Cannot be used with string or floating point types.

```c++
switch (x) {
	case 0:
		break;
	case 1:
	case 2:
		// Falling through
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
vector<int> arr = {1, 2, 3, 4};

for(int num : arr) {
	cout << num << endl;
}
```

## [Functions](#c)
- Functions cannot be declared within other functions.
- You have to declare a function before using it. There is no hoisting

| Term           | Example              |
|----------------|----------------------|
| header         | `void func(int arg)` |
| prototype      | `void func(int);`    |
| implementation | Body of the func     |

- The purpose of the prototype being put above main is to allow the function definition to be used after the main function.

### [Types of functions](#c)

|                          |                                                                       |
|--------------------------|-----------------------------------------------------------------------|
| `constexpr void func();` | Return value is consts so it can be evaluated at compile time         |
| `inline void func();`    | Compiler searches and replaces. Speed up performance, but more memory |

### [Reference arguments](#c)
- You can make function arguments pass by reference by setting them as `&`
- Reference arguments have to have an address so they cannot be values.

```c++
void assignX(int &x) { // x is a reference parameter
	// This & is slightly different to the use case of getting the address
	x = 10;
}

void assignY(int *y) { // y is a pointer to an int
	*y = 10;
}

int x, y;
assignX(x); // x is now 10
assignY(&y); // y is now 10
```

- If you want to pass in a `const` you have to specify it in the argument.
	- Ex: `void assignX(const int &x);`
- An array argument is equivalent to a pointer to the first element of the array.
	- `void func(int arr[]);` is the same as `void func(int *arr);`
	- There is no special syntax in c++ for pass by value for an array argument.

### [Optional arguments](#c)
- Everything after the first optional arguments must also be optional arguments.

```c++
int test(int a, int b = 4, int c = 10){
	// c is an optional argument
}

test(1, 2, 3);
test(1, 2);
test(1);
```

- If you have a prototype you can only put the default values in the prototype

### [Function overloading](#c)
- Function overloading are multiple functions with the same name, but different argument types.
	- The compiler determines which function to call based on the argument types.
- Functions that return different types don't overload.

## [Custom Scope](#c)
- You can use `{}`s to define custom scope

```c++
{
	int x = 10;
	cout << x << endl;
}
{
	double x = 10.1;
	cout << x << endl;
}
```

## [Global and static variables](#c)
- Global variables are variables outside of any function
- Global variables are automatically set to 0 if not given a value
- Global variables should be used sparingly because they can cause side effects, like hidden parameters, in function.
	- Usually global variables are consts in order to prevent these side effects.

- `static` allows a local variable to persist across function calls.

```c++
for(int i = 0; i< 10; i++){
	callFunc();
}

void callFunc() {
	static int count = 0;
	count++;
	cout << count << endl;
}
```

## [Exception/Error handling](#c)
If your program has an error and you want to crash you can do: `std::cerr << "An error occured\n"` which prints an error and `exit(1);` which exits the program with a 1(`#include <stdio.h>`). But what if you want to continue running your code even when there's an error?

In C, you commonly return `-1` or `NULL` to show there was an error, but there are two main problems with this.

1. Complicated return types
- Let's say you have a function that reads a file and returns a string of the contents of that file, but that function has an error. You could return `"-1"`, but that could be confused with the contents of the file. You could wrap the return string in an optional and return `{}` when there's an error, but that is very messy. You could pass in a reference parameter that gets set when there's an error, but that is also messy. All of these solutions aren't ideal.

2. Bubbling up errors
- Let's say you have func1 which calls func2 which calls func3. And let's say there's an error in fun3 and it returns `-1`. In order for func1 to get the error, there has to be error handling code in func2 which checks for the error and returns it to func1 if it's there. This is very annoying, especially if the error has to bubble through many function layers.

In order to solve these two problems specific error handling keywords were introduced: `try`, `catch`, and `throw`.

1. Solves complicated return types
- Instead of all the messy solutions to return your error, you can instead `throw` an error and it doesn't have to match the type the function is returning.
- It simplifies the return types for your functions and return additional information along with the error.

2. Solves bubbling up errors
- Instead of having special error handling code in all your functions, a thrown error automatically bubbles up until it reaches a `catch` block for it's error type. `throw` is essentially a multi-level return.
- Separates your algorithm code from your error handling code.

<table>
<tr>
	<th>Without <code>try</code>, <code>catch</code>, and <code>throw</code></th>
	<th>With <code>try</code>, <code>catch</code>, and <code>throw</code></th>
</tr>
<tr>
	<td>

```C++
int func3() {
	bool error = true;
	if (error) {
		return -1;
	}
}

int func2() {
	int error = func3();
	if (error == -1) {
		return -1;
	}
}

void func1() {
	int error = func2();
	if (error == -1) {
		// Handle error
	}
}
```

</td>
<td>

```C++
void func3() {
	bool error = true;
	if (error) {
		throw -1;
	}
}

void func2() {
	func3();
}

void func1() {
	try {
		func2();
	} catch (int error) {
		// Handle error
	}
}
```

</td>
</tr>
</table>

- If an error is thrown and not caught, the program crashes.
- `catch` blocks can be strung together and are caught in order, so you should catch more specific exceptions before less specific ones.
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

```C++
void handleErrors() {
	try {
		throw; // Throws the last error
	} catch (const std::bad_alloc& e) {

	} catch (const std::invalid_argument& e) {

	} catch (const std::exception& e) {

	}
}

void func() {
	try {
			// Code that may throw an exception
	} catch (...) {
			// Catches all errors
			handleErrors();
	}
}
```
