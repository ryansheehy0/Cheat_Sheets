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

# Sort Algorithms
Sorting algorithms take in an array and sorts them from lowest to highest, highest to lowest, alphabetical, or any other such way.

<!-- TOC -->

- [Common sorting algorithm](#common-sorting-algorithm)
- [Bubble Sort](#bubble-sort)
- [Selection Sort](#selection-sort)
- [Quick Sort](#quick-sort)

<!-- /TOC -->

## [Common sorting algorithm](#sort-algorithms)
- O(n^2)
  - Bubble sort
  - Selection sort
  - Insertion sort
- O(n log n)
  - Merge sort
  - Quick sort(Third fastest)
  - Heap sort
- Other
  - Tim Sort(Second fastest)
    - Optimized merger sort
  - Intro sort(Fastest)
    - Uses heap sort for large lengths, medium lengths it uses quick sort, and small lengths it used insertion sort.
  - Count Sort
    - Counts the number of occurrences of each element then reconstructs the sorted array from that count.
  - Shell sort
  - Bucket sort
  - Radix Sort

## [Bubble Sort](#sort-algorithms)
Loop through each element, compares adjacent elements, and swaps them if they are in the wrong order. This continues until no more swaps are needed.

```javascript
function bubbleSort(arr){
  let swap = true
  while(swap){
    swap = false
    for(let i = 0; i < arr.length - 1; i++){
      if(arr[i] > arr[i+1]){
        // Swap
        let temp = arr[i]
        arr[i] = arr[i+1]
        arr[i+1] = temp
        swap = true
      }
    }
  }
  return arr
}
```

## [Selection Sort](#sort-algorithms)
Finds the largest(or smallest) element in the unsorted section of the array, swaps it with the first unsorted element, and continues this gradually building a sorted portion at the beginning of the array.

```javascript
function findMaxIndex(arr){
  let largest = arr[0]
  let largestIndex = 0
  for(let i = 1; i < arr; i++){
    if(arr[i] > largest){
      largest = arr[i]
      largestIndex = i
    }
  }
  return largestIndex
}

function selectionSort(arr){
  for(let i = 0; i < arr.length; i++){
    let maxIndex = findMaxIndex(arr.slice(i)) + i
    let temp = arr[i]
    arr[i] = arr[maxIndex]
    arr[maxIndex] = temp
  }
  return arr
}
```

## [Quick Sort](#sort-algorithms)
Select a pivot(usually the last element) and splits the array in two, according to whether they are less than or greater than the pivot. These sub-arrays are recursively sorted, and the results are combined to make the sorted array.

```javascript
function quickSort(arr) {
  if (arr.length === 1) return arr

  const pivot = arr[arr.length - 1]
  let left = []
  let right = []

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)]
}
```