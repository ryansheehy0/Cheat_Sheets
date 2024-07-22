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

# Unique Permutations
Algorithm to get all the unique permutations of an array.

```
            ___________0,1,2___________
           /             |             \
        0,1,2          1,0,2          2,1,0
       /     \        /     \        /     \
    0,1,2   0,2,1  1,0,2   1,2,0  2,1,0   2,0,1
```

```javascript
let arr = ["0", "1", "2"]

function getUniquePermutations(arr){
	let uniquePermutations = []

	function recursivePermutations(arr, unswappedIndex){
		if(unswappedIndex === arr.length - 1){
			uniquePermutations.push([...arr])
			return
		}
		for(let i = unswappedIndex; i < arr.length; i++){
			// Swap
			let temp = arr[unswappedIndex]
			arr[unswappedIndex] = arr[i]
			arr[i] = temp
			recursivePermutations(arr, unswappedIndex + 1)
			// Unswap
			temp = arr[unswappedIndex]
			arr[unswappedIndex] = arr[i]
			arr[i] = temp
		}
	}

	recursivePermutations(arr, 0)
	return uniquePermutations
}

console.log(getUniquePermutations(arr))

/*
[
  [ '0', '1', '2' ],
  [ '0', '2', '1' ],
  [ '1', '0', '2' ],
  [ '1', '2', '0' ],
  [ '2', '1', '0' ],
  [ '2', '0', '1' ]
]
*/
```