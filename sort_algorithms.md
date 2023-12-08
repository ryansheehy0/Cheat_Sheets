[Home](./README.md)

# Sort Algorithms
Sorting algorithms take an input and sort them from lowest to highest, highest to lowest, alphabetical, or any other such way.

The output should be the sorted input.

## Table of Contents

<!-- TOC -->

- [Sort Algorithms](#sort-algorithms)
  - [Table of Contents](#table-of-contents)
  - [Quadratic](#quadratic)
    - [Bubble Sort](#bubble-sort)
    - [Selection Sort](#selection-sort)
    - [Insertion Sort](#insertion-sort)
  - [Comparison](#comparison)
    - [Quick Sort](#quick-sort)
    - [Shell Sort](#shell-sort)
    - [Merge Sort](#merge-sort)
    - [Heap Sort](#heap-sort)
    - [Bucket Sort](#bucket-sort)
  - [Linear](#linear)
    - [Radix Sort](#radix-sort)
    - [Counting Sort](#counting-sort)
  - [Hybrid](#hybrid)
  - [Tim Sort](#tim-sort)

<!-- /TOC -->

## [Quadratic](#table-of-contents)

### [Bubble Sort](#table-of-contents)
Goes through one element at a time, compares the adjacent element, and swaps them if they are in the wrong order.
- O(n^2)
  - Small datasets ok-ish
  - Large datasets bad

[1, 4, 2, 3]
Compare 1 and 4
  1 is less than 4 so move to the next element(4)
Compare 4 and 2
  4 is greater than 2 so swap
  [1, 2, 4, 3]
  Compare 4 and 3
    4 is greater than 3 so swap
    [1, 2, 3, 4]
    4 is at the end so move back to the beginning(1)
Compare 1 and 2
  1 is less than 2 so move to the next element(2)
Compare 2 and 3
  2 is less than 3 so move to the next element(3)
3 is at the end so move back to the beginning(1)
Compare 1 and 2
  1 is less than 2 so move to the next element(2)
2 is at the end so move back to the beginning(1)
1 is at the end and at the beginning so sorting is done

```javascript
const input = [1, 4, 2, 3]

function bubbleSort(input){
  let loopLength = input.length
  for(let i = 0; i <= loopLength; i++){
    if(i < loopLength){ // If i isn't at the last element
      if(input[i] < input[i+1]){
        // move to the next element
        continue
      }else{
        // swap places
        const temp = input[i]
        input[i] = input[i+1]
        input[i+1] = temp
      }
    }else{ // If i is at the last element
      loopLength--
      i = 0 // restart for loop
    }
  }
  return input
}

console.log(bubbleSort(input))
```

### [Selection Sort](#table-of-contents)
Divides input into 2 categories. Sorted and unsorted region. Finds the smallest(or largest) in the unsorted and moves it into the sorted region.
O(n^2)

### [Insertion Sort](#table-of-contents)
Divides input into 2 categories. Sorted and unsorted region. Takes one elements from the unsorted and inserts it into its correct position in the sorted region.
O(n^2)

## [Comparison](#table-of-contents)
A comparison sorting algorithm compares two at a time using either < or > operators.

### [Quick Sort](#table-of-contents)
Quicksort defines a pivot(usually at the end) and sorts the array so that elements to the left are less than the pivot and elements to the right are greater than the pivot. This is then done recursively to the left and right sides until there is no longer anything to sort.
- O(n log n)
- Worst case: O(n^2)
- Memory usage: O(log n) due to recursion

input is [4, 1, 2, 5, 3]
Pivot is the last element(3). i is -1 and j is 0
Is 4(input[j]) less than 3(input[pivot])
  No so increment j(1)
Is 1 less than 3
  Yes so increment i(0)
  Swap 4(input[i]) and 1(input[j])
  Increment j(2)
[1, 4, 2, 5, 3]
Is 2 less than 3
  Yes so increment i(1)
  Swap 4 and 2
  Increment j(3)
[1, 2, 4, 5, 3]
Is 5 less than 3
  No so increment j(4)
J is the same location as the pivot
  so place 3 at input[i+1]
[1, 2, 3, 4, 5]
Recursively apply the quick sort algorithm to the left([1, 2]) and right([4, 5]) sides of the pivot
  Do this until there is only one element

```javascript
const input = [4, 1, 2, 5, 3]

function quickSort(input){
  if(input.length === 1 || input.length === 0) return input // Recursion end case

  let i = -1
  let j = 0
  const lastIndex = input.length - 1
  const pivot = input[lastIndex] // Pass by value
  while(j !== lastIndex){
    if(input[j] < pivot){
      i++
      // swap
      const temp = input[j]
      input[j] = input[i]
      input[i] = temp
    }
    j++
  }
  i++
  // place pivot
  input.splice(i, 0, pivot) // insert pivot at i
  input.length-- // remove last element
  // Quick sort left and right
  const leftArray = input.slice(0, i)
  const rightArray = input.slice(i+1, input.length)
  const sortedLeftArray = [...quickSort(leftArray)] // Pass by value
  const sortedRightArray = [...quickSort(rightArray)] // Pass by value

    // Replace left array
  input.splice(0, leftArray.length, ...sortedLeftArray)
    // Replace right array
  input.splice(i+1, rightArray.length, ...sortedRightArray)

  return input
}

console.log(quickSort(input))
```

### [Shell Sort](#table-of-contents)
O(n log n)

### [Merge Sort](#table-of-contents)
### [Heap Sort](#table-of-contents)
### [Bucket Sort](#table-of-contents)

## [Linear](#table-of-contents)

### [Radix Sort](#table-of-contents)

O(n)

### [Counting Sort](#table-of-contents)
The count sort algorithm goes through the input and counts how many of a digit there are and then reconstructs the sorted array from that count.
- O(n)
- This sorting algorithm is best when the range is known before hand and the difference between each element isn't great


The input is [1, 0, 2, 2, 4, 1]
The range is between 0 and 4
Go through one element at a time
Count array:   [1, 2, 2, 0, 1]
Number counted: 0  1  2  3  4
Output: [0, 1, 1, 2, 3, 4]

```javascript
const input = [1, 0, 2, 2, 4, 1]

function arrayWithZeros(length){
  let array = []
  for(let i = 0; i < length; i++){
    array.push(0)
  }
  return array
}

function countingSort(input, min = Math.min(...input), max = Math.max(...input)){
  let countArray = new Array(max - min)
  // Set the count array
  input.forEach(ele => {
    countArray[ele - min]++
  })
  // Construct output array from the count array
  let outputArray = new Array(input.length)
  countArray.forEach((ele, index) => {
    for(let i = 0; i < ele; i++){
      outputArray[ian] =WithZeros index + m + 1in
    }
  })
  return outputArray
}

console.log(countingSort(input, 0, 4))
```

## [Hybrid](#table-of-contents)
.push()

## [Tim Sort](#table-of-contents)
