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

# Memory Managed Hash Table

- Arrays are slow to retrieve data(high computations), but take up only the memory that is needed(low memory).
- Hash tables are fast at retrieving data(low computations), but take up a lot of memory to allow all possible states of the hash output(high memory).
- What if you could put the data in an array(low memory) and encode the position of that data in an equation. Then when retrieving the data you just have to run the equation(low computations) to get the exact position.

## Table of Contents

<!-- TOC -->

- [Memory Managed Hash Table](#memory-managed-hash-table)
	- [Table of Contents](#table-of-contents)
	- [Getting data](#getting-data)
	- [Putting data](#putting-data)
	- [How do you update the equation with the data and the index?](#how-do-you-update-the-equation-with-the-data-and-the-index)
	- [How do you update the equation when removing data?](#how-do-you-update-the-equation-when-removing-data)

<!-- /TOC -->

## [Getting data](#table-of-contents)
1. Plug data into the retrieval equation
2. Get the index of the data from the equation

## [Putting data](#table-of-contents)
1. Put data into the array and get the index
2. Update the equation with the data and the index

## [How do you update the equation with the data and the index?](#table-of-contents)

## [How do you update the equation when removing data?](#table-of-contents)
