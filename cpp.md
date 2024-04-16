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

[Home](./README.md)

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
	- [Headers](#headers)
	- [Namespaces](#namespaces)
	- [Character escapes](#character-escapes)
	- [Including libraries](#including-libraries)
	- [Common libraries](#common-libraries)
	- [Points and addresses](#points-and-addresses)
	- [Order of operations](#order-of-operations)

<!-- /TOC -->

## Things to research
- `<<` and `>>` operator. Stream operators?

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
		- Use `''` for 1 character and `""` for 1 or more characters
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
- You can use `'` to separate long numbers. Ex: `1'999'999`
- When dividing, if you want the result to be a float, then one of the values has to be a float. Ex: `1/2` will return `0`, but `1.0/2` or `1/2.0` will return `0.5`
- `0.0/0.0` outputs not a number(nan), `1.0/0.0` outputs inf, `-1.0/0.0` outputs -inf.
- You can represent floats in scientific notation `6.08e2` is `6.08 x 10^2` which is `608`. Or `6.08e-2` for `0.0608`
	- It is recommended to start floats with `0` instead of a `.`

### [Modifiers](#table-of-contents)
	- unsigned
	- signed
		- By default data types are signed
	- const
		- By convention use snake case with all capital letters

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

## [Including libraries](#table-of-contents)
What's the difference between `<>`s and `""`s for including?

## [Common libraries](#table-of-contents)
You can find libraries at `https://cplusplus.com/reference/<library>`

- iostream
	- `std::cout << "Hello world!";` - Characters out. prints to console
	- `std::cout << std::endl;` - End line. clears buffer of cout. The next cout will be on a new line.
	- `std::cin >> var` - Characters in. Gets user input from terminal.
- string
	- `std::string test = "test";`
- cmath
	- C++ doesn't have operator for exponential. `std::pow(base, exponent)`
	- `%` only works for integer based data types
	- Use defined `M_PI` to use pi
- iomanip
	- `std::cout << std::fixed << std::setprecision(2) << value;` - Rounds any floats to display with 2 values after the decimal point. Doesn't change value of float.

## [Points and addresses](#table-of-contents)
Declaring
- Ex: `int* myPointer`
	- myPointer contains enough memory to hold an address and points to an int. It has to point to an int.

Referencing
- `&myPointer` gets the address of myPointer.
- `myPointer` gets the value in myPointer, which is the memory address it holds (the address it points to).
- `*myPointer` dereferences myPointer and gets the value of the integer variable it points to.

## [Order of operations](#table-of-contents)

| Order | Operation                  |
|-------|----------------------------|
| 1     | Inside ()s                 |
| 2     | unary -. Negate a variable |
| 3     | * / %                      |
| 4     | + -                        |
| 5     | left to right              |

