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

## Table of Contents
<!-- TOC -->

- [C++](#c)
	- [Table of Contents](#table-of-contents)
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
			- [Comparing floats](#comparing-floats)
			- [Interment post-fix vs pre-fix](#interment-post-fix-vs-pre-fix)
		- [Variable Modifiers](#variable-modifiers)
		- [Casting](#casting)
		- [Auto and typeid](#auto-and-typeid)
	- [Headers](#headers)
	- [Namespaces](#namespaces)
	- [Character escapes](#character-escapes)
	- [Common libraries](#common-libraries)
		- [iostream](#iostream)
			- [Repeatedly ask for user input](#repeatedly-ask-for-user-input)
		- [string](#string)
		- [cmath](#cmath)
			- [Random numbers](#random-numbers)
		- [cstdlib](#cstdlib)
		- [iomanip](#iomanip)
		- [vector](#vector)
		- [typeinfo](#typeinfo)
		- [fstream](#fstream)
	- [Pointers and references](#pointers-and-references)
		- [Function pointers](#function-pointers)
	- [Order of operations](#order-of-operations)
	- [Switch](#switch)
	- [Functions](#functions)
		- [Reference arguments](#reference-arguments)
		- [Optional arguments](#optional-arguments)
		- [Function overloading](#function-overloading)
	- [Scope](#scope)
	- [Loops](#loops)
	- [Global variables](#global-variables)
	- [Header files](#header-files)
	- [Arrays](#arrays)
	- [Conditions and loops on one line](#conditions-and-loops-on-one-line)
		- [Static variables](#static-variables)
	- [Getting each digit](#getting-each-digit)

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

- `"a"` outputs a null terminated array of characters, while `'a'` is just that character.
	- `"a"` is the same as `['a', '\0']`

## [main](#table-of-contents)
`main()` is the start of the program.

`int main(int argc, char **argv){}`

- `return 0;` tells the program that main returned without any errors.
- `return 1;` tells the program that main returned with an error.

## [Data Types](#table-of-contents)
The smallest memory unit is 1 byte(8 bits).

### [Int based data types](#table-of-contents)

| Name      | Bytes  | Notes                                        |
|-----------|--------|----------------------------------------------|
| bool      | 1      | Can use `true` or `false` keywords           |
| char      | 1      | Uses `''`s                                   |
| wchar_t   | 2 or 4 | Larger char encoding standards like unicode. |
| short     | 2      | Same as `short int`                          |
| int       | 2 or 4 | Bytes depends on the platform                |
| long long | 8      | Same as `long long int`                      |

### [Float based data types](#table-of-contents)

| Name        | Bytes |
|-------------|-------|
| float       | 4     |
| double      | 8     |
| long double | 12    |

### [Data type notes](#table-of-contents)

#### [Truthy and Falsy](#table-of-contents)
- Anything positive or negative is truthy
- `0` is not falsy
- `(x = #)` returns `x` not `#`
	- Ex: `x = 10` returns `10`
	- Ex: `x = 0` returns `0`
	- Ex: `x = 2'147'483'648` returns `-2147483648`

#### [Multiple variables on one line](#table-of-contents)
- Declaring multiple variables on one line
	- `int x, y;`
- Setting multiple variables on one line
	- `int x = 10, y = 20;`
- Assigning multiple variables on one line
	- `x = y = 20;`
	- `x` and `y` will both be equal to `20`
- Command equals multiple variables
	- `x += x + 3;` is the same as `x = x + x + 3;`

#### [Variable names / Identifiers](#table-of-contents)
- Variable names can only use letters, underscores, and digits, and cannot start with digits.
	- Ex: `_this_is_a_valid_variable_name`
- Variable names are case sensitive

#### [Assigning values](#table-of-contents)
- You can use `'` to separate long numbers.
	- Ex: `1'999'999`
- You can assign floats using scientific notation.
	- `6.08e2` = `6.08 x 10^2` = `608`
	- `6.08e-2` = `0.0608`
- It is recommended to start floats with `0` instead of a `.`

#### [Int vs Float Division](#table-of-contents)
- Integer division
	- Division without the remainder
- Float division
	- Division with the remainder
	- In order to get float division, either the numerator or denominator has to be a float/double.
- Ex: `1/2` will return `0`
- Ex: `1.0/2` will return `0.5`
- Ex: `1/2.0` will return `0.5`
- Ex: `1.0/2.0` will return `0.5`

#### [Dividing by zero](#table-of-contents)
- Integer division
	- Gives a compiler error
- Float division
	- `0.0/0.0` outputs not a number(nan)
	- `1.0/0.0` outputs inf
	- `-1.0/0.0` outputs -inf

#### [Int vs Float Modulus](#table-of-contents)
- Compiler error if you use modulus with floats/doubles.
- Modulus can only work with int data types

#### [Comparing floats](#table-of-contents)
- Don't use `x == y` because floats can be imprecise
- Use `fabs(x - y) < 0.0001` instead

#### [Interment post-fix vs pre-fix](#table-of-contents)
- `x++` returns `x` then increments it by 1
- `++x` increments `x` then returns `x`

### [Variable Modifiers](#table-of-contents)
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

### [Casting](#table-of-contents)
- Casting is done at compiler time so it's up to the programmer to make sure they are casting correctly
- `static_cast<data type>(variable)`
- Int value gets cast to a double
	- Ex: `1 -> 1.0`
- Float values get cast to an int by removing everything after the decimal
	- Ex: `1.9 -> 1`

### [Auto and typeid](#table-of-contents)
- `auto` tells the compiler to determine the variable's type by the initial value given
	- Ex: `auto x = "apple";` gets assigned const char*
	- Ex: `auto x = 0.01;` gets assigned double
- Has to be initialized or else it will throw an error

## [Headers](#table-of-contents)
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

## [Namespaces](#table-of-contents)
What are namespaces and what are they used for?

`using namespace std;`

- To access a namespace use the `namespace::command`.

## [Character escapes](#table-of-contents)

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

## [Common libraries](#table-of-contents)
You can find libraries at `https://cplusplus.com/reference/<library>`

### [iostream](#table-of-contents)

|                            |                                                     |
|----------------------------|-----------------------------------------------------|
| `std::cout << "string";`   | Output to console                                   |
|                            | Floats don't output `.0`. `99` not `99.0`           |
| `std::cout << std::endl;`  | Outputs new line. Same as `\n`                      |
| `std::cin >> var`          | User input from console                             |
|                            | Inputs are separated by white spaces                |
|                            | If user enters an invalid input it returns false    |
|                            | Keeps new lines in the buffer                       |
| `std::cin >> var1 >> var2` | Multiple inputs on one line                         |
| `std::cin.ignore()`        | Ignores the next character                          |
| `std::cin.get()`           | Gets the next character in the buffer including new |

#### [Repeatedly ask for user input](#table-of-contents)

```c++
while(true) {
	if(!(cin >> input) || /*input isn't valid*/) {
		cout << "Please try again" << endl;
		cin.clear(); // Clears cin errors
		while (cin.get() != '\n'); // Removes the previous input
		continue;
	}

	// Do stuff
	break;
}
```

### [string](#table-of-contents)

|                                    |                                               |
|------------------------------------|-----------------------------------------------|
| `std::string str = "str";`         | If not initialized it will be an empty string |
| `std::getline(std::cin, str);`     | Gets all remaining text in the current buffer |
|                                    | Gets up to the next new line                  |
|                                    | Doesn't include the new line in str           |
|                                    | Removes the ending new line in the buffer     |
| `str.size()`                       |                                               |
| `str.at(index)`                    | returns char                                  |
| `str.replace(index, length, str2)` | Replaces starting at index                    |
| `str.find(str2)`                   | Gets the starting index of the string         |
|                                    | Returns `string::npos` if nothing was found   |

### [cmath](#table-of-contents)
- Floating point math operations

|                            |                                    |
|----------------------------|------------------------------------|
| `std::pow(base, exponent)` |                                    |
| `std::sqrt(x)`             |                                    |
| `std::fabs(x)`             | absolute value                     |
| `std::ceil(x)`             | Round up                           |
| `std::floor(x)`            | Round down                         |
| `std::rand()`              | Random int from `0` and `RAND_MAX` |
| `M_PI`                     |                                    |

#### [Random numbers](#table-of-contents)
- `std::rand() % 10` between 0-9
- `(std::rand() % 11) + 20` between 20-30

### [cstdlib](#table-of-contents)
- Integer math operations

|               |                        |
|---------------|------------------------|
| `std::abs()`  |                        |
| `std::atoi()` | Converts string to int |

### [iomanip](#table-of-contents)

|                                  |                                              |
|----------------------------------|----------------------------------------------|
| `cout << std::fixed`             | `setprecision` counts after decimal point    |
| `cout << std::setprecision(num)` | Limits float digits                          |
|                                  | Continually active                           |
|                                  | Rounds the output                            |
| `cout << std::setw(10)`          | Sets width of output                         |
|                                  | Only valid for the value directly after `<<` |
|                                  | Aligns output to the right side              |
|                                  | Value larger than `setw` then it ignored     |
| `cout << std::right;`            | Justify right                                |
| `cout << std::left;`             | Justify left                                 |


- `cout << setprecision(2) << 9.99999;`
	- Ex: `10`
- `cout << fixed << setprecision(2) << 9.99999;`
	- Ex: `10.00`
- If no fixed and exceeds bounds of `setprecision`, then it's outputted in scientific notation
	- Ex: `cout << setprecision(2) << 146.789;` outputs `1.5e+02`

### [vector](#table-of-contents)
- Dynamic arrays in c++
- `std::vector<int> nums = {0, 1, 2};`
- `nums[0] = 10;`
- `nums.push_back(3);` Adds 3 to the end of the vector

### [typeinfo](#table-of-contents)
- `typeid(var).name()` gives a string of the type of variable.

| returned | Type     |
|----------|----------|
| `d`      | double   |
| `c`      | char     |
| `i`      | integer  |
| `P`      | pointer  |
| `K`      | constant |

### [fstream](#table-of-contents)
- Reading and writing to files

|                             |                     |
|-----------------------------|---------------------|
| `ifstream`                  | Reading file        |
| `ofstream`                  | Writing file        |
| `fstream`                   | Reading and writing |
| `fstream file("name.txt");` | Open file           |
| `file.open("name.txt");`    | Also opens the file |
| `file.close();`             | Closes a file       |
| `file.is_open()`            | Checks if it opened |

- A file acts like a regular buffer
	- `file << "concatenate";`
	- `file >> input;`
	- `getline(file, line);`

## [Pointers and references](#table-of-contents)

|               |                                         |
|---------------|-----------------------------------------|
| `int* ptr;`   | Contains enough memory to store address |
| `&ptr`        | Gets address of pointer                 |
| `ptr`         | Gets the value in ptr                   |
| `*ptr`        | Dereferences ptr                        |
| `int& x = y;` | When `x` is assigned `y` also changes   |

### [Function pointers](#table-of-contents)
`void (*name)(int, int) = function`

## [Order of operations](#table-of-contents)

| Order | Operation                  |
|-------|----------------------------|
| 1     | x++ x-- function calls     |
| 2     | Inside ()s                 |
| 3     | !                          |
| 4     | unary -. Negate a variable |
| 5     | * / %                      |
| 6     | + -                        |
| 7     | left to right              |
| 8     | < <= > >=                  |
| 9     | == !=                      |
| 10    | &&                         |
| 11    | \|\|                       |

## [Switch](#table-of-contents)
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

You tend to make the cases constants.

```c++
const int ZERO = 0;

switch (x) {
	case ZERO:
		break;
	// etc
}
```

## [Functions](#table-of-contents)
- Functions cannot be declared within functions
- You have to declare a function before using it.
	- There is no hoisting
- `constexpr void func();`, which indicates that the return value of the function is a constant value can be computed at compile time.
- `inline void func();`
	- Compiler searches and replaces that function. Can speed up performance because you don't have to call the function
- Terms
	- The **header** is the function's return type, name, and arguments.
		- Ex: `void func(int test)`
	- The **prototype** is used before main so that you can define it after main.
		- It doesn't have the argument names.
		- Ex: `void func(int);`
	- The **implementation** is the body fo the function

### [Reference arguments](#table-of-contents)
You can make function arguments pass by reference by setting them as `&`
- Multiple pass by reference parameters makes sense when the output values are intertwined

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

- References arguments must have an address so they cannot be `const`s or values.
- If you do want to pass in a `const` you have to specify in the argument.
	- Ex: `void assignX(const int &x)`
	- Adding `const` is promising the compiler that you aren't changing that argument's value.

### [Optional arguments](#table-of-contents)
```c++
int test(int a, int b = 4, int c = 10){
	// c is an optional argument
}
```

- All default arguments need to be placed at the end.
	- Everything after a default argument must also have a default
- If you have a prototype you can only put the default values in the prototype

### [Function overloading](#table-of-contents)
- Functions with the same name, but different argument types.
- The compiler determines which function to call based on the argument types.
- Functions that return the different types, but have the same argument types don't trigger function overloading and give a compiler error.

## [Scope](#table-of-contents)
- You can use `{}`s to define scope

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

## [Loops](#table-of-contents)
- Do While loops are often used to ask the user repeatedly for input

```c++
int userInput;
do {
	cout << "Enter password: ";
	cin >> userInput;
} while(userInput != 2023);
```

- You don't need the {}s for for loops or while loops if they only contain 1 statement.

```c++
for(int i = 0; i< 10; i++)
	cout << i << endl;

while (true)
  cout << "infinity ";
```

## [Global variables](#table-of-contents)
- Global variables are variables outside any function
- Global variables should be used sparingly because they can cause side effects in function.
	- Side effects are another function updating a variable which effect another function. Like a hidden parameter.
	- Usually global variables are constants in order to prevent these side effects.

## [Header files](#table-of-contents)
- Allows you to initialize functions after the main function because all the function definitions are already declared.
	- Function definitions are also called function prototypes
		- `void func(int, int);`

## [Arrays](#table-of-contents)
- You don't have to specify the length of the array if you are declaring and initializing it at the same time.
	- `char name[] = "ryan";`
	- `int ages[] = {1, 2, 3};`

## [Conditions and loops on one line](#table-of-contents)
- You can do if statements and if-else on one line without the curly brackets
```c++
if (x == 1)
	cout << x;

// or
if (x == 1) cout << x;

if (x != 1) cout << "false";
else cout << x;
```

### [Static variables](#table-of-contents)
`static` local variables persist across function calls.

Ex: 
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
## [Getting each digit](#table-of-contents)
- Used to get each digit
```c++
int temp = val;
ones = val % 10;
temp = val / 10;

tens = val % 10;
temp = val / 10;

hundreds = val % 10;
```

- Global variables are always init with 0 if you don't give it a value
- Ex: `int arr[5] = {1};`
	- The rest will be init to 0
- Ex: `int arr[5];`
	- Unknown what's inside the array
- Segmentation fault
	- Going outside of your program's segment set by the OS