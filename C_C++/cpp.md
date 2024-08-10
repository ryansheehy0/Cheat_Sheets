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
		- [Variable names / Identifiers](#variable-names--identifiers)
		- [Assigning values](#assigning-values)
		- [Int vs Float Division](#int-vs-float-division)
		- [Dividing by zero](#dividing-by-zero)
		- [Int vs Float Modulus](#int-vs-float-modulus)
		- [Getting each digit](#getting-each-digit)
		- [Comparing floats](#comparing-floats)
		- [Interment post-fix vs pre-fix](#interment-post-fix-vs-pre-fix)
	- [Variable Modifiers](#variable-modifiers)
	- [Casting](#casting)
	- [Auto and typeid](#auto-and-typeid)
- [Headers](#headers)
- [Namespaces](#namespaces)
- [Character escapes](#character-escapes)
- [Pointers and references](#pointers-and-references)
	- [Function pointers](#function-pointers)
- [Order of operations](#order-of-operations)
- [Switch](#switch)
- [Functions](#functions)
	- [Types of functions](#types-of-functions)
	- [Reference arguments](#reference-arguments)
	- [Optional arguments](#optional-arguments)
	- [Function overloading](#function-overloading)
- [Custom Scope](#custom-scope)
- [Do While loops](#do-while-loops)
- [Single line conditions](#single-line-conditions)
- [Global and static variables](#global-and-static-variables)
- [Arrays](#arrays)
- [Range based for loop](#range-based-for-loop)

<!-- /TOC -->

## Things to research
- `<<` and `>>` operator. Stream operators?
	- Overloading operators
- How is string different from char*
- Fill out regex for c++
- What's the difference between including with `<>`s and `""`s?
- string vs char* vs char[]
- reference vs pointer
- Can you overload the main function
	- You cannot overload main
- What does replace length do? For string library
- Header files allows you to initialize functions after the main function because all the function definitions are already declared.
	- Function definitions are also called function prototypes
		- `void func(int, int);`

- Segmentation fault
	- Going outside of your program's segment set by the OS

- `"a"` outputs a null terminated array of characters, while `'a'` is just that character.
	- `"a"` is the same as `['a', '\0']`

## [main](#c)
`main()` is the start of the program.

`int main(int argc, char **argv){}`

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
- Anything positive or negative is truthy
- `0` is not falsy
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

#### [Variable names / Identifiers](#c)
- Variable names can only use letters, underscores, and digits, and cannot start with digits.
	- Ex: `_this_is_a_valid_variable_name`
- Variable names are case sensitive

#### [Assigning values](#c)
- You can use `'` to separate long numbers.
	- Ex: `1'999'999`
- You can assign floats using scientific notation.
	- `6.08e2` = `6.08 x 10^2` = `608`
	- `6.08e-2` = `0.0608`
- It is recommended to start floats with `0` instead of a `.`

#### [Int vs Float Division](#c)
- Integer division
	- Division without the remainder
- Float division
	- Division with the remainder
	- In order to get float division, either the numerator or denominator has to be a float/double.
- Ex: `1/2` will return `0`
- Ex: `1.0/2` will return `0.5`
- Ex: `1/2.0` will return `0.5`
- Ex: `1.0/2.0` will return `0.5`

#### [Dividing by zero](#c)
- Integer division
	- Gives a compiler error
- Float division
	- `0.0/0.0` outputs not a number(nan)
	- `1.0/0.0` outputs inf
	- `-1.0/0.0` outputs -inf

#### [Int vs Float Modulus](#c)
- Compiler error if you use modulus with floats/doubles.
- Modulus can only work with int data types

#### [Getting each digit](#c)

```c++
int temp = val;
ones = temp % 10;
temp = temp / 10;

tens = temp % 10;
temp = temp / 10;

hundreds = temp % 10;
```

#### [Comparing floats](#c)
- Don't use `x == y` because floats can be imprecise
- Use `fabs(x - y) < 0.0001` instead

#### [Interment post-fix vs pre-fix](#c)
- `x++` returns `x` then increments it by 1
- `++x` increments `x` then returns `x`

### [Variable Modifiers](#c)
- `unsigned`
- `signed`
	- By default data types are signed
- `const`
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
- Int value gets cast to a double
	- Ex: `1 -> 1.0`
- Float values get cast to an int by removing everything after the decimal
	- Ex: `1.9 -> 1`

### [Auto and typeid](#c)
- `auto` tells the compiler to determine the variable's type by the initial value given
	- Ex: `auto x = "apple";` gets assigned const char*
	- Ex: `auto x = 0.01;` gets assigned double
- Has to be initialized or else it will throw an error

## [Headers](#c)
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

## [Namespaces](#c)
What are namespaces and what are they used for?

`using namespace std;`

- To access a namespace use the `namespace::command`.

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

## [Switch](#c)
- Cannot be used with string or floating point types.

```c++
switch (x) {
	case 0:
		break;
	case 1:
		break;
	case 2:
	case 3:
		// Falling through
		break;
	default:
		break;
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

## [Do While loops](#c)

```c++
do {
} while(true);
```

## [Single line conditions](#c)

```c++
if(true)
	cout << "true" << endl;

if (true)
	cout << "true" << endl;
else
	cout << "false" << endl;

for(int i = 0; i < 10; i++)
	cout << i << endl;

while (true)
  cout << "infinity ";
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

## [Arrays](#c)

```c++
int arr[3]; // Don't know what it's initialized with
int arr[3] = {1}; // Initialized with {1, 0, 0}
int arr[] = {1, 0, 0}; // Size is 3
```

- The name of the array is like a constant pointer.
	- It always points to the first element of the array.

```c++
const int arr[3] = {0, 1, 2}
// Have to initialize it
// Can't change any of the values in the array
```

## [Range based for loop](#c)
- It isn't recommended to use because it has some restrictions
	- Can only be used in the same scope where the array is created

```c++
int arr[] = {1, 2, 3, 4};

for(int &num : arr) {
	num++;
}

for(int num : arr) {
	cout << num << endl;
}
```