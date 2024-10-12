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

# Programming Tips
Instructions for common operations in programming. This uses C++, but can be applied to any language.

<!-- TOC -->

- [Organization tips](#organization-tips)
- [Repeatedly ask for user input](#repeatedly-ask-for-user-input)
- [Swapping variables without a temp variable](#swapping-variables-without-a-temp-variable)
- [Getting each digit of an int](#getting-each-digit-of-an-int)
- [Comparing floats](#comparing-floats)
- [Getting random numbers](#getting-random-numbers)

<!-- /TOC -->

## [Organization tips](#programming-tips)
- Use composition over inheritance
  - Composition is putting a parent object in the child class.
	- https://www.youtube.com/watch?v=hxGOiiR9ZKg
- Design in Minimum Viable Products(MVP) stages.
  - Finish priority features instead of working on features you want to work on
- It is almost always better to start coding then to worry too much about how to organize the code.

## [Repeatedly ask for user input](#programming-tips)
Ask for user input, validate it, and if it isn't correct ask again.

```c++
int input;
while (true) {
  cout << "User input: ";
  if (!(cin >> input) || !(/*Check if input is valid*/)) {
    cout << "Please try again.\n";
    cin.clear(); // Clear error flags
    continue;
  }
  break;
}
```

## [Swapping variables without a temp variable](#programming-tips)

```c++
// Swap a and b
int a = 50, b = 10;

a = a ^ b;
b = a ^ b;
a = a ^ b;

cout << "a: " << a << endl;
cout << "b: " << b << endl;
```

## [Getting each digit of an int](#programming-tips)

```c++
int var = 12345;
vector<int> digits;

int temp = var;
for (int i = 0; temp != 0; i++) {
  digits.push_back(temp % 10);
  temp /= 10;
}
```

## [Comparing floats](#programming-tips)
- You cannot use `x == y` because floats are imprecise.
- Use `fabs(x - y) < 0.0001` instead.

## [Getting random numbers](#programming-tips)
Getting a random number from a range using a function that generates numbers from 0 to 1, `rand()`.

```c++
int getRandomNum(int start, int end) { // Both are inclusive
  return (rand() % (end - start + 1)) + start;
}
```

- `rand() % 10` between 0-9
- `(rand() % 11) + 20` between 20-30