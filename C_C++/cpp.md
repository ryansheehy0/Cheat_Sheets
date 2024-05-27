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

## Table of Contents
<!-- TOC -->

- [C++](#c)
	- [Table of Contents](#table-of-contents)
	- [Things to research](#things-to-research)
	- [main](#main)
	- [Data Types](#data-types)
		- [Data type notes](#data-type-notes)
		- [Modifiers](#modifiers)
		- [Casting](#casting)
			- [static_cast](#static_cast)
		- [Auto and typeid](#auto-and-typeid)
	- [Headers](#headers)
	- [Namespaces](#namespaces)
	- [Character escapes](#character-escapes)
	- [Common libraries](#common-libraries)
		- [iostream](#iostream)
		- [string](#string)
			- [string vs char* vs char[]](#string-vs-char-vs-char)
		- [cmath](#cmath)
		- [cstdlib](#cstdlib)
		- [iomanip](#iomanip)
		- [vector](#vector)
		- [regex](#regex)
		- [typeinfo](#typeinfo)
		- [fstream](#fstream)
	- [Pointers, addresses, and references](#pointers-addresses-and-references)
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

<!-- /TOC -->

## Things to research
- `<<` and `>>` operator. Stream operators?
	- Overloading operators
- How is string different from char*
- Fill out regex for c++
- What's the difference between including with `<>`s and `""`s?
- string vs char* vs char[]

## [main](#table-of-contents)
`main()` is the start of the program.

`int main(int argc, char **argv){}`

`return 0;` tells the program that main returned without any errors.

## [Data Types](#table-of-contents)
The smallest memory unit is 1 byte(8 bits).

- Int based
	- bool
		- 1 byte
		- Anything positive or negative is truthy
		- Can use `true` and `false` keywords
	- char
		- 1 byte
		- Uses `''`
	- wchar_t
		- 2 or 4 bytes
		- Use to represent larger character encoding standards. Usually unicode.
	- short
		- 2 bytes
		- This is the same as `short int`
	- int
		- 4 bytes
		- Might be 2 bytes. Depends on the platform and compiler.
	- long long
		- 8 bytes/64 bits
		- This is the same as `long long int`
- Float based
	- float
		- 4 bytes
	- double
		- 8 bytes/64 bits
	- long double
		- 12 bytes/96 bits

### [Data type notes](#table-of-contents)
- You can set multiple variables on one line.
	- `int x = 10, y = 20;`
- Names can only use letters, underscores, and digits, and cannot start with digits.
	- C++ is case sensitive
	- Ex: `_this_is_a_valid_variable_name`

- Assigning values
	- You can use `'` to separate long numbers. Ex: `1'999'999`
	- You can represent floats in scientific notation `6.08e2` is `6.08 x 10^2` which is `608`. Or `6.08e-2` for `0.0608`
		- It is recommended to start floats with `0` instead of a `.`

- When dividing, if you want the result to be a float, then one of the values has to be a float. Ex: `1/2` will return `0`, but `1.0/2` or `1/2.0` will return `0.5`
- `x += x + 3;` is the same as `x = x + x + 3;`
- `x = 10` returns 10, `x = 0` returns 0, `x = 2'147'483'648` returns -2147483648
	- `(x = #)` returns `x` not `#`.

- You can do if statements and if-else on one line without the curly brackets
```c++
if (x == 1)
	cout << x;

// or
if (x == 1) cout << x;

if (x != 1) cout << "false";
else cout << x;
```

- Dividing by 0
	- `0.0/0.0` outputs not a number(nan), `1.0/0.0` outputs inf, `-1.0/0.0` outputs -inf.
	- If `0` is in the denominator it will give a runtime error.
	- `%` gives an error when used with floating point values. If the denominator is `0` it gives a runtime error.


- Used to get each digit
```c++
int temp = val;
ones = val % 10;
temp = val / 10;

tens = val % 10;
temp = val / 10;

hundreds = val % 10;
```

- Comparing
	- Don't use the `==` operator to compare floating point types due to their imprecision.
		- Use `fabs(x - y) < 0.0001` instead of `x == y`
	- You can compare strings. `myString == "test"`
	- You can use ternary operators: `condition ? value_if_true : value_if_false`

- `x++` vs `++x`
	- `x++` returns `x` then increments it by 1
	- `++x` increments `x` then returns `x`

### [Modifiers](#table-of-contents)
- unsigned
- signed
	- By default data types are signed
- const
	- By convention use snake case with all capital letters
	- By convention declare and init consts before any other variables
	- Use `const` over `#define`
		- If necessary, modern compilers do the same thing as substituting and replacing
		- Gain type checking and syntax checking
		- Known to the debugger
		- Scoped to the block where they are defined

### [Casting](#table-of-contents)
Different types of casting
	- static_cast
	- dynamic_cast
	- const_cast
	- reinterpret_cast
	- c style casting

- C++ can perform implicit type conversion for converting between an int and a double when either operand is a double for arithmetic operators(like +, *, etc) or for assigning(4 -> 4.0 or 4.9 -> 4).

#### [static_cast](#table-of-contents)
```c++
int integer1 = 1;
int integer2 = 2;
double dbl = static_cast<double>(integer1) / integer2;
	// Converts one fo the integers to a double so the result will contain decimals
```

Casting that is done at compile time.
	- Doesn't perform any runtime checking so it's up to the program to ensure that it's safe.

### [Auto and typeid](#table-of-contents)
`auto` tells the compiler to determine the variable's type by the initial value given. It has to be initialized or else it will throw an error.

This can be useful for more complex data types.

- `auto x = "apple";` gets assigned the type const char*
- `auto x = 0.01;` gets assigned ot a double

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
- `std::cout << "Hello world!";` - Characters out. prints to console
	- Doesn't output any trailing zeros when outputting a floating point values. Output 99 not 99.0
- `std::cout << std::endl;` - End line. clears buffer of cout. The next cout will be on a new line.
- `std::cin >> var` - Characters in. Gets user input from terminal.
	- Separates each input by whitespace
	- Ignores the leading white space. Ex: input `Hi there`, first cin would be `Hi` and second would be `there`.
	- Keeps new lines in the buffer
	- You can do it on all one line. `std::cin >> var1 >> var2 >> var3;`
	- Returns false when the input isn't valid into the variable.
		- Returns false when overflowing input

```c++
// Infinitely ask the user for input
int num;
while(true){
	cout << "Enter num: " << endl;
	if(cin >> num){
		cout << "You entered: " << num << endl;
	}else{
		cin.clear();
		// Remove the new line
		string temp;
		getline(cin, temp);
		cout << "You can't enter that. Please try again." << endl;
	}
}
```

- `cin.ignore()` used to ignore the next character, usually a `\n` from the input buffer.
- `cin.get()` gets the next character in the input buffer
	- Used to get any character from input buffer including an enter.

### [string](#table-of-contents)
- `std::string test = "test";`
	- If not initialized it is automatically initialized to an empty string.
- `"a"` outputs a null terminated array of characters, while `'a'` is just that character.
	- `"a"` is the same as `['a', '\0']`
- `std::getline(std::cin, str);` - gets all remaining text on the current input line, up to the next newline character which isn't included into str.
	- Includes leading whitespace
	- Removes the ending new line in the buffer
- `<string>.size()`
- `<string>.at(index)` returns a char
- `<string>.replace(index, length, replacement_string)`
- `<string>.find(string)` gets the starting index of string
	- returns `string::npos` if nothing was found

#### [string vs char* vs char[]](#table-of-contents)

### [cmath](#table-of-contents)
- Math operations for floating point values
- C++ doesn't have operator for exponential. `std::pow(base, exponent)`
- `std::sqrt(x)`, `std::fabs(x)` absolute value, `std::ceil(x)` round up, `std::floor(x)` round down, `std::rand()` random integer between `0` and 	`RAND_MAX`.
	- `std::rand() % 10` between 0-9, `std::rand() % 101` between 0-100, `(std::rand() % 11) + 20` between 20-30
- Use defined `M_PI` to use pi

### [cstdlib](#table-of-contents)
- Math operations for integer values and some other functionality
- `std::abs()`, `std::atoi()` converts strings(like "5") to ints.

### [iomanip](#table-of-contents)
- `std::cout << std::fixed << std::setprecision(2) << value;`
	- Rounds any float/double to display with 2 values after the decimal point. Doesn't change value of float.
	- If you don't have fixed it starts counting from the left most digit instead of the decimal place.
		- If you don't have fixed, and your number is greater than what's set by `setprecision`, it will round and add `e+##`
			- Ex: `int x = 146.789; cout << setprecision(2);` it will output `1.5e+02`
	- Active to everything coming after it.
- `std::cout << std::setw(10) << var << endl;` sets the width of output.
	- Aligns output with the right side
	- If the var outputs characters larger than what's in `setw` then the `setw` will be ignored
	- Active to only the thing after the `<<`
- `defaultfloat()` resets `setprecision`
- `std::right` and `std::left` can be used to justify the next output to the left or right.

```c++
double x = 149.89;
double y = 24.2;
double z = 1.783;

cout << setw(10) << setprecision(2) << x << endl;
cout << defaultfloat();
cout << setw(10) << y << endl;
cout << setw(10) << z;

/*
   1.5e+02
	 24.2
*/
```

### [vector](#table-of-contents)
- Dynamic arrays in c++
- `std::vector<int> nums = {0, 1, 2};`
- `nums[0] = 10;`
- `nums.push_back(3);` Adds 3 to the end of the vector

### [regex](#table-of-contents)

### [typeinfo](#table-of-contents)
- `typeid(var).name()` gives a string of the type of variable.
	- `d` for double, `c` for char, `i` for integer.
	- `P` for pointer, `K` for constant

### [fstream](#table-of-contents)
- Reading

```c++
ifstream file("filename.txt");
string line;
file >> line;
// or
getline(file, line);
file.close();
```

- Creating and writing

```c++
ofstream file("filename.txt");
file << "Concatenate";
file.close();
```

- Both

```c++
fstream file("filename.txt");
file << "Concatenate";
string line;
file >> line;
file.close();
```

## [Pointers, addresses, and references](#table-of-contents)
Declaring
- Ex: `int* myPointer`
	- myPointer contains enough memory to hold an address and points to an int. It has to point to an int.

Referencing
- `&myPointer` gets the address of myPointer.
- `myPointer` gets the value in myPointer, which is the memory address it holds (the address it points to).
- `*myPointer` dereferences myPointer and gets the value of the integer variable it points to.

You can reference other variables with `&`
- `int& x = y;` means that if x is assigned it also changes the value of y.

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

### [Optional arguments](#table-of-contents)
```c++
int test(int a, int b = 4, int c = 10){
	// c is an optional argument
}
```

- All default arguments need to be placed at the end.

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