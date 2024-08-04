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

## Table of Contents

<!-- TOC -->

- [Programming Tips](#programming-tips)
	- [Table of Contents](#table-of-contents)
	- [Swapping variables without temp variable](#swapping-variables-without-temp-variable)
	- [GPLv3 License](#gplv3-license)
		- [How to add GPLv3 License](#how-to-add-gplv3-license)
	- [Project Management](#project-management)
	- [Formatting and Rules](#formatting-and-rules)
	- [Code Organization](#code-organization)
	- [When to reuse code](#when-to-reuse-code)

<!-- /TOC -->

## [Swapping variables without temp variable](#table-of-contents)

```c++
// Swap a and b
int a = 50, b = 10;

a = a ^ b;
b = a ^ b;
a = a ^ b;

cout << "a: " << a << endl;
cout << "b: " << b << endl;
```

## [GPLv3 License](#table-of-contents)
If you are making your code open source, then it is recommended to use the GPLv3 license in order to prevent other companies from taking your work, adding some feature/modifications, and then selling or distributing their own closed sourced version of your code.
- Why open source is good?
  - Prevent undiscovered bugs. More reliable applications.
  - Allows for anyone to contribute to your project.

### [How to add GPLv3 License](#table-of-contents)
1. Include a copy of the license at the root of your project named `COPYING`
2. Add a licensing notice at the top of each of your source code files
  - Make sure to replace "THIS PROGRAM" with the name of your program.

```javascript
/*
 * This file is part of THIS PROGRAM.
 *
 * THIS PROGRAM is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * THIS PROGRAM is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with THIS PROGRAM. If not, see <https://www.gnu.org/licenses/>.
 */
```

3. Add `THIS PROGRAM is licensed under GPLv3. See the COPYING file for details.` to your README.md under `## License`
4. Include a copy of the license with the distribution of your software.

## [Project Management](#table-of-contents)
- Have a well detailed end goal app idea
  - A full write up on how all the features are going to work and how each page of the app will look and work
- Develop in stages of Minimum Viable Products(MVPs)
  - MVP 1, MVP 2, etc. Keep adding MVPs until you reach all the features in the end goal app idea
  - The 1st MVP should be the most bare bones features as possible. Just the minimum to make it somewhat usable.
  - The last 20-10% of your MVP will be integration hell and finding any edge cases where you code breaks
- Delegate tasks and every few days or week have a group meeting on the progress of those tasks
  - If one member is falling behind then put more resources to help them catch up

## [Formatting and Rules](#table-of-contents)
- No space between ()s and {s
- Use 's instead of "s
- When assigning variables use spaces between the `=`s
- Use guard clauses when possible
- When possible use variables and self explanatory code instead of comments
  - Sometimes it maybe necessary to write your pseudo-code before beginning, but if done the unnecessary comments should be removed after the code is done.
  - If you need to use comments have no spaces between comments and code

## [Code Organization](#table-of-contents)
It is almost always better to get started coding with bad organization and then organize your code when you can clearly see the patterns.

- Use function to re-use code
- If a class has a lot of methods brake out those methods into separate classes in a folder called main_subclasses
```
item
  item.js
  item_subclasses
    events.js
```
- If 2 or more classes share a significant amount of code use inheritance in a folder called main_children
```
item
  item.js
  item_children
    list.js
    card.js
```

## [When to reuse code](#table-of-contents)
Always be hesitant to re-use code.

It is better to change the same code in multiple places then it is to pass more and more information between the parent and child.

It is better to change the same code in multiple places then it is to completely reorganize your code in order to add a new feature.
  - This is especially important when it comes to re-using separate components/classes.
  - Over time small changes become larger and larger. This creates more and more complexity as the reused component it given more and more information to distinguish between its different roles.

## Never use inheritance
- You cannot use inheritance in Neo-C
	- https://www.youtube.com/watch?v=hxGOiiR9ZKg
	- Maybe instead of you cannot, you should not.