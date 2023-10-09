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

## Quadratic

### Bubble Sort
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

### Selection Sort
Divides input into 2 categories. Sorted and unsorted region. Finds the smallest(or largest) in the unsorted and moves it into the sorted region.
O(n^2)

### Insertion Sort
Divides input into 2 categories. Sorted and unsorted region. Takes one elements from the unsorted and inserts it into its correct position in the sorted region.
O(n^2)

## Comparison

### Quick Sort
O(n log n)

### Shell Sort
O(n log n)

### Merge Sort
### Heap Sort
### Bucket Sort

## Linear

### Radix Sort
O(n)

### Counting Sort

## Hybrid

## Tim Sort