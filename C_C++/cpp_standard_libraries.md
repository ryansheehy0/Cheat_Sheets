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

# C++ Standard Libraries
You can find libraries at `https://cplusplus.com/reference/<library>`

## Table of Contents
<!-- TOC -->

- [C++ Standard Libraries](#c-standard-libraries)
	- [Table of Contents](#table-of-contents)
	- [iostream](#iostream)
		- [Repeatedly ask for user input](#repeatedly-ask-for-user-input)
	- [string](#string)
	- [cmath](#cmath)
		- [Random numbers](#random-numbers)
		- [ctime](#ctime)
	- [cstdlib](#cstdlib)
	- [iomanip](#iomanip)
	- [vector](#vector)
	- [typeinfo](#typeinfo)
	- [fstream](#fstream)
	- [cctype](#cctype)

<!-- /TOC -->

## [iostream](#table-of-contents)

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
| `.ignore()`                | Ignores the next character                          |
| `.get(ch)`                 | Gets the next character in the buffer including new |
| `.clear()`                 | Clears the flags include end of file(eof) flag      |

- `.seekg(offset, std::ios_base::beg)`
	- Sets the position of the input pointer for the stream
	- Ex: `file.seekg(0, ios_base::beg);`

### [Repeatedly ask for user input](#table-of-contents)

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

## [string](#table-of-contents)

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

## [cmath](#table-of-contents)
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

### [Random numbers](#table-of-contents)
- `std::rand() % 10` between 0-9
- `(std::rand() % 11) + 20` between 20-30

### [ctime](#table-of-contents)
- `#include <ctime>`
- `srand(time(0));`
	- Sets the seed for random number

## [cstdlib](#table-of-contents)
- Integer math operations

|               |                        |
|---------------|------------------------|
| `std::abs()`  |                        |
| `std::atoi()` | Converts string to int |

## [iomanip](#table-of-contents)

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

## [vector](#table-of-contents)
- Dynamic arrays in c++
- `std::vector<int> nums = {0, 1, 2};`
- `nums[0] = 10;`
- `nums.push_back(3);` Adds 3 to the end of the vector

## [typeinfo](#table-of-contents)
- `typeid(var).name()` gives a string of the type of variable.

| returned | Type     |
|----------|----------|
| `d`      | double   |
| `c`      | char     |
| `i`      | integer  |
| `P`      | pointer  |
| `K`      | constant |

## [fstream](#table-of-contents)
- Reading and writing to files

|                             |                                  |
|-----------------------------|----------------------------------|
| `ifstream`                  | Reading file                     |
| `ofstream`                  | Writing file                     |
|                             | Don't need to check if it's open |
| `fstream`                   | Reading and writing              |
| `fstream file("name.txt");` | Open file                        |
| `file.open("name.txt");`    | Also opens the file              |
| `file.close();`             | Closes a file                    |
| `file.is_open()` and `file` | Checks if it opened              |

- A file acts like a regular buffer
	- `file << "concatenate";`
	- `file >> input;`
	- `getline(file, line);`

## [cctype](#table-of-contents)

|                 |                        |
|-----------------|------------------------|
| `tolower(char)` | Converts to lower case |