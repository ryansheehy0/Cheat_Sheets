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

The standard libraries are any library that uses namespace std.
- It's assumed that `using std namespace;` is being used.

<!-- TOC -->

- [iostream](#iostream)
- [string](#string)
- [cmath](#cmath)
	- [ctime](#ctime)
- [cstdlib](#cstdlib)
- [iomanip](#iomanip)
- [vector](#vector)
- [typeinfo](#typeinfo)
- [fstream](#fstream)
- [cctype](#cctype)
- [optional](#optional)
- [Data Containers](#data-containers)
	- [array](#array)
	- [vector](#vector)
	- [list](#list)
	- [[deque]](#deque)
	- [set](#set)
	- [map](#map)
- [Algorithms](#algorithms)

<!-- /TOC -->

## [iostream](#c-standard-libraries)

|                       |                                                     |
|-----------------------|-----------------------------------------------------|
| `cout << "string";`   | Output to console                                   |
|                       | Floats don't output `.0`. `99` not `99.0`           |
| `cout << endl;`       | Outputs new line. Same as `\n`                      |
| `cin >> var`          | User input from console                             |
|                       | Inputs are separated by white spaces                |
|                       | If user enters an invalid input it returns false    |
|                       | Keeps new lines in the buffer                       |
| `cin >> var1 >> var2` | Multiple inputs on one line                         |
| `.ignore()`           | Ignores the next character                          |
| `.get(ch)`            | Gets the next character in the buffer including new |
| `.clear()`            | Clears the flags include end of file(eof) flag      |

- `.seekg(offset, std::ios_base::beg)`
	- Sets the position of the input pointer for the stream
	- Ex: `file.seekg(0, ios_base::beg);`

## [string](#c-standard-libraries)

|                                    |                                               |
|------------------------------------|-----------------------------------------------|
| `string str = "str";`              | If not initialized it will be an empty string |
| `getline(cin, str);`               | Gets all remaining text in the current buffer |
|                                    | Gets up to the next new line                  |
|                                    | Doesn't include the new line in str           |
|                                    | Removes the ending new line in the buffer     |
| `str.size()`                       |                                               |
| `str.at(index)`                    | returns char                                  |
| `str.replace(index, length, str2)` | Replaces starting at index                    |
| `str.find(str2)`                   | Gets the starting index of the string         |
|                                    | Returns `string::npos` if nothing was found   |

## [cmath](#c-standard-libraries)
- Floating point math operations

|                       |                                    |
|-----------------------|------------------------------------|
| `pow(base, exponent)` |                                    |
| `sqrt(x)`             |                                    |
| `fabs(x)`             | absolute value                     |
| `ceil(x)`             | Round up                           |
| `floor(x)`            | Round down                         |
| `rand()`              | Random int from `0` and `RAND_MAX` |
| `M_PI`                |                                    |

### [ctime](#c-standard-libraries)
- `#include <ctime>`
- `srand(time(0));`
	- Sets the seed for random number

## [cstdlib](#c-standard-libraries)
- Integer math operations

|          |                        |
|----------|------------------------|
| `abs()`  |                        |
| `atoi()` | Converts string to int |

## [iomanip](#c-standard-libraries)

|                             |                                              |
|-----------------------------|----------------------------------------------|
| `cout << fixed`             | `setprecision` counts after decimal point    |
| `cout << setprecision(num)` | Limits float digits                          |
|                             | Continually active                           |
|                             | Rounds the output                            |
| `cout << setw(10)`          | Sets width of output                         |
|                             | Only valid for the value directly after `<<` |
|                             | Aligns output to the right side              |
|                             | Value larger than `setw` then it ignored     |
| `cout << right;`            | Justify right                                |
| `cout << left;`             | Justify left                                 |

- `cout << setprecision(2) << 9.99999;`
	- Ex: `10`
- `cout << fixed << setprecision(2) << 9.99999;`
	- Ex: `10.00`
- If no fixed and exceeds bounds of `setprecision`, then it's outputted in scientific notation
	- Ex: `cout << setprecision(2) << 146.789;` outputs `1.5e+02`

## [vector](#c-standard-libraries)
- Dynamic arrays in c++
- `vector<int> nums = {0, 1, 2};`
- `nums[0] = 10;`
- `nums.push_back(3);` Adds 3 to the end of the vector

## [typeinfo](#c-standard-libraries)
- `typeid(var).name()` gives a string of the type of variable.

| returned | Type     |
|----------|----------|
| `d`      | double   |
| `c`      | char     |
| `i`      | integer  |
| `P`      | pointer  |
| `K`      | constant |

## [fstream](#c-standard-libraries)
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

## [cctype](#c-standard-libraries)

|                 |                        |
|-----------------|------------------------|
| `tolower(char)` | Converts to lower case |

## [optional](#c-standard-libraries)
Optional is used when there is the possiility that you cannot get any code back?

```C++
optional<string> openFile(string fileName) {
	fstream file(fileName);
	if (!file) return {} // No data

	string contents;
	stringstream contents_stream;
	contents_stream << file.rdbuf();
	contents = contents_stream.str();
	file.close();

	return contents;
}

int main() {
	optional<fstream> file = openFile("test.cpp");
	if (!file){
		cout << "Error opening test.cpp" << endl;
		return 1;
	}
}
```

- There's the `optionalVar.value_or(value)` which returns the value in optionalVar if it's there or the value inside the `()`s if it's not.

## [Data Containers](#c-standard-libraries)

| Operation    | Speed                 |
|--------------|-----------------------|
| Reading      | Fast                  |
| Inserting    | Slow                  |
| Appending    | Fast                  |
| Getting size | Done at compiler time |

- Is there a linked list of arrays?

### [array](#c-standard-libraries)
`std::array<type, size>` is used to store a block of continuous memory. This has advantages over the regular C style arrays because it supports iterators, error handing for reading/writing out of bounds, and allows you to easily get the size(size is calculated at compile time).
- Advantages
	- Fast random access
	- Automatically stored on the stack
- Disadvantages
	- Can't change size
	- Slow to insert/delete

.

### [vector](#c-standard-libraries)
`std::vector<type>` is an array that can grow in size. First a fixed size array is stored in the heap. If an insert would overflow the array, a new larger fixed size array is created else where in the heap, and all the contents of the smaller array are moved to the larger array.
- Advantages
	- Fast random access
	- Can change size
- Disadvantages
	- You can't have a pointer to an element in the vector because it can change locations if the vector grows in size.
	- Slow to insert/delete
		- Can have reallocation costs

.push_back()
.size()
.pop_back()
.empty()
.clear()
.insert(iterator pos, element)
.erase(iterator pos)
.resize()
.reserve()
.capacity() - returns the number of elements that the vector can hold before needing to allocate more memory
.data() vs &vec[0]?

.begin() vs .front()
.end() vs .back()

### [list](#c-standard-libraries)
`std::list<type>` is a doubly linked list stored in the heap. Each node stores a pointer to its parent and child node.
- Advantages
	- Quick to insert/remove
	- Can change size
	- Easily splice multiple lists together
- Disadvantages
	- Slow random access
	- High memory overhead

### [deque]
`std::deque<type>` is a linked list of arrays. This sort of mixes the advantages and disadvantages of a list and vector.
- Advantages
	- Can change size
	- Quick to 
	- Fast memory access
- Disadvantages
	- High memory overhead

.push_back
.push_front

- Double ended que
- Index table. Does the required calculations to convert a direct access index to the correct location in the deque.

### [set](#c-standard-libraries)
`std::set<type>` and `std::unordered_set<type>` are used to store a list of unique elements. Set automatically sorts the elements as they go in, but unordered doesn't.

.insert()
.find()

### [map](#c-standard-libraries)
`std::map<keyType, valueType>` and `std::unordered_map<keyType, valueType>` are used to store a list of key value pairs.

```C++
mp["key"] = value;
```

- They return a `std::pair` which has two properties of `.first` and `.second`.

## [Algorithms](#c-standard-libraries)
- std::algorithm