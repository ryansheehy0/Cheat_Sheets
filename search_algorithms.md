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

# Search Algorithms
This cheatsheet is referring to input as the input data structure(usually an array), the value as the value you're being asked to find in the input data structure, and the output as the index of the value in the input.

If no value is found in the input the search algorithm usually returns -1

## Table of Contents

<!-- TOC -->

- [Search Algorithms](#search-algorithms)
	- [Table of Contents](#table-of-contents)
	- [Linear Search](#linear-search)
	- [Binary Search](#binary-search)
	- [Interpolation Search](#interpolation-search)

<!-- /TOC -->

## [Linear Search](#table-of-contents)
Linear search goes through each element and checks to see if it's the value.
- O(n) linear time
  - Slow for large input sizes
  - Good for small/medium input sizes
- Input doesn't need to be sorted
- Good for inputs without random access like linked lists

```javascript
const array = [9, 1, 8, 2, 7, 3, 6, 4, 5]

function linearSearch(input, value){
  for(let i = 0; i < input.length; i++){
    if(input[i] === value) return i
  }
  return -1
}

console.log(linearSearch(array, 4)) // 7
```

## [Binary Search](#table-of-contents)
Binary search splits the input array in half and repeats this until there is only 1 value left. If you are dividing an odd lengthed array you tend to round down.
- O(log n)
  - Slow for small input sizes
  - Fast for large input sizes
- Input needs to be sorted
- Input data structure needs to support random access like arrays

```javascript
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9]

function binarySearch(input, value){
  let left = 0
  let right = input.length - 1

  while(left <= right){
    const mid = Math.floor((left + right) / 2)
    const midValue = input[mid]

    if(midValue === value) return mid

    if(midValue < value){
      left = mid + 1
    }else{
      right = mid - 1
    }
  }
  return -1
}

console.log(binarySearch(array, 4)) // 3
```

## [Interpolation Search](#table-of-contents)
An interpolation search is the binary search, but instead of checking the center it makes an educated guess(probe) where the value would be in the input.

This best guess(probe) is gotten by using linear interpolation.
- The Y is the indexes of the array. The X is the values in the array.
  - $y_1$ = left, $x_1$ = input[left]
  - $y_2$ = right, $x_2$ = input[right]
  - $x$ = value, $y$ = probe
- First, find the slope. $m = \frac{y_1 - y_2}{x_1 - x_2}$
- Second, make a line from the slope. $y = y_1 + m(x-x_1)$
- The equation for a slope and the line are combined to form the equation for probe.

Linear interpolation is best used for uniformly distributed inputs.
- Average case: O(log(log n))
- Worst case: O(n)
- Input needs to be sorted
- Input data structure needs to support random access like arrays

```javascript
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9]

function interpolationSearch(input, value){
  let left = 0
  let right = input.length - 1

  while(left <= right){
    const probe = left + (left - right) * (value - input[left]) / (input[left] - input[right])
    const probeValue = input[probe]

    if(probeValue === value) return probe

    if(probeValue < value){
      left = probe + 1
    }else{
      right = probe - 1
    }
  }
  return -1
}

console.log(binarySearch(array, 4)) // 3
```

- Instead of linear interpolation, if you know the input follows a different patter, you can use other equations instead of a line.