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
		- [Modifiers](#modifiers)
	- [Namespaces](#namespaces)
	- [Character escapes](#character-escapes)
	- [Including libraries](#including-libraries)
	- [Common libraries](#common-libraries)
		- [iostream](#iostream)
		- [string](#string)
		- [cmath](#cmath)

<!-- /TOC -->

## Things to research
- `<<` and `>>` operator. Stream operators?

## [main](#table-of-contents)
`main()` is the start of the program.

`return 0;` tells the program that main returned without any errors.

## [Data Types](#table-of-contents)
The smallest memory unit is a byte(8 bits).

- Int based
	- bool - 1 byte
		- Anything positive or negative is truthy
		- Can use `true` and `false` keywords
	- char - 1 byte/8 bits
		- use `''` for 1 character
		- use `""` for 1 or more characters
	- wchar_t - 2 or 4 bytes
		- Use to represent larger character encoding standards. Usually unicode.
	- short - 2 bytes/16 bits
		- This is the same as `short int`
	- int - 4 bytes/32 bits
	- long long - 8 bytes/64 bits
		- This is the same as `long long int`
- Float based
	- float - 4 bytes
	- double - 8 bytes/64 bits
	- long double - 12 bytes/96 bits

You can set multiple variables on one line.
- `int x = 10, y = 20;`

### [Modifiers](#table-of-contents)
	- unsigned
	- signed
		- By default data types are signed

## [Namespaces](#table-of-contents)
What are namespaces and what are they used for?

`using namespace std;`

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
- string
- cmath

### [iostream](#table-of-contents)
`#include <iostream>`

`std::cout << "Hello world!";` - Characters out. prints to console
`std::cout << std::endl;` - End line. clears buffer of cout. The next cout will be on a new line.
`std::cin >> var` - Characters in. Gets user input from terminal.

### [string](#table-of-contents)
`#include <string>`

`std::str test = "test";`

### [cmath](#table-of-contents)
`#include <cmath>`

- C++ doesn't have operator for exponential. `std::pow(base, exponent)`
- `%` only works for integer based data types
