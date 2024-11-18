[Home](../README.md)

# C++ Data Structures, Iterators, and Algorithms

<!-- TOC -->

- [Data Structures](#data-structures)
	- [array](#array)
	- [vector](#vector)
	- [list](#list)
		- [Linked Lists](#linked-lists)
	- [deque](#deque)
	- [set](#set)
	- [map](#map)
- [Iterators](#iterators)
	- [Constant iterators](#constant-iterators)
	- [Different types of iterators](#different-types-of-iterators)
	- [back_inserter](#back_inserter)
- [Algorithms](#algorithms)
	- [Sort](#sort)

<!-- /TOC -->

## [Data Structures](#c-data-structures-iterators-and-algorithms)
- std::array
- std::vector
- Linked lists
	- std::list
	- std::forward_list
- std::deque
- Sets
	- std::set
	- std::unordered_set
	- std::multiset
	- std::unordered_multiset
- Maps(Uses hashing in the background)
	- std::map
	- std::unordered_map
	- std::multimap
	- std::unordered_multimap
- std::string

| Operation    | Speed                 |
|--------------|-----------------------|
| Reading      | Fast                  |
| Inserting    | Slow                  |
| Appending    | Fast                  |
| Getting size | Done at compiler time |

| Data Type   | Stack/Heap | Fast reading/writing | Fast inserting/removal |
|-------------|------------|----------------------|------------------------|
| Array       | Stack      | Fast                 | Slow                   |
| Vector      | Heap       | Fast                 | Slow                   |
| Linked List | Heap       | Slow                 | Fast                   |

- Is there a linked list of arrays?

### [array](#c-data-structures-iterators-and-algorithms)
`std::array<type, size>` is used to store a block of continuous memory. This has advantages over the regular C style arrays because it supports iterators, error handing for reading/writing out of bounds, and allows you to easily get the size(size is calculated at compile time).
- Advantages
	- Fast random access
	- Automatically stored on the stack
- Disadvantages
	- Can't change size
	- Slow to insert/delete

### [vector](#c-data-structures-iterators-and-algorithms)
`std::vector<type>` is an array that can grow in size. First a fixed size array is stored in the heap. If an insert would overflow the array, a new larger fixed size array is created else where in the heap, and all the contents of the smaller array are moved to the larger array.
- Advantages
	- Fast random access
	- Can change size
- Disadvantages
	- You can't have a pointer to an element in the vector because it can change locations if the vector grows in size.
	- Slow to insert/delete
		- Can have reallocation costs

| Method                            | Description                                                    |
|-----------------------------------|----------------------------------------------------------------|
| .at(size_type n)                  | Get reference to element at n index                            |
| .size()                           | Get how many elements are in the vector                        |
| .empty()                          | Checks if the vector is empty or not                           |
| .clear()                          | Removes all the elements                                       |
| .push_back(const T& x)            | Adds new element to end of vector                              |
| .erase(iterator pos)              | Removes element. Higher elements are shifted back to fill gap. |
| .insert(iterator pos, const T& x) | Copies x to element at pos. Higher elements are shifted over.  |
| .begin()                          | Returns an iterator to the first element.                      |
| .end()                            | Returns an iterator to one past the last element.              |

.pop_back()
.resize()
.reserve()
.capacity() - returns the number of elements that the vector can hold before needing to allocate more memory
.data() vs &vec[0]?

.begin() vs .front()
.end() vs .back()

- Dynamic arrays in c++
- `vector<int> nums = {0, 1, 2};`
- `nums[0] = 10;`
- `nums.push_back(3);` Adds 3 to the end of the vector

### [list](#c-data-structures-iterators-and-algorithms)
`std::list<type>` is a doubly linked list stored in the heap. Each node stores a pointer to its parent and child node.
- Advantages
	- Quick to insert/remove
	- Can change size
	- Easily splice multiple lists together
- Disadvantages
	- Slow random access
	- High memory overhead

- You have two classes. ListNode and List
- When inserting a new node, you have to assign the new node's next node to the next, and then assign the prev's next node to the new node.

```C++
// Get each element of the linked list
ListNode* currNode = _head;
while (currNode != nullptr) {
	// So something with currNode
	currNode = currNode->nextNode();
}
```

- Arrays/vectors are quick at getting and updating, but slow at removing and adding.
	- If sorted you can use binary or interpolated search which is very fast.
	- When you add or remove you have to shift elements around so they stay in continuous memory.
- Linked lists are quick at removing and adding, but slow at getting and updating.
	- You can only update and get elements with linear search.


- Get/Find
	- Only linear search
- Delete
	- Save the prt to the node you want to delete
	- Assign the prev node's next node to the deleted node's next ptr
	- Delete the node you want to delete
- Add
	- Assign the new node's next node
	- Assign the prev node's next node to the new node
- Update
	- Find and then change value

### [deque](#c-data-structures-iterators-and-algorithms)
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

### [set](#c-data-structures-iterators-and-algorithms)
`std::set<type>` and `std::unordered_set<type>` are used to store a list of unique elements. Set automatically sorts the elements as they go in, but unordered doesn't.

.insert()
.find()

### [map](#c-data-structures-iterators-and-algorithms)
`std::map<keyType, valueType>` and `std::unordered_map<keyType, valueType>` are used to store a list of key value pairs.

```C++
mp["key"] = value;
```

- They return a `std::pair` which has two properties of `.first` and `.second`.
## [Iterators](#c-data-structures-iterators-and-algorithms)
Iterators are used to standardize access to elements across different underlying data structures. `.begin()` returns an iterator to the first element of the container, and `.end()` returns an iterator to one element past the last element of the container.
- You cannot access `.end()` because it isn't pointing to any element.
- It redefines certain operations so they can work c-style arrays.
	- This isn't OOP programming because it separated the functions from the data. Generic programming.
- Iterators are a common interface for different algorithms to apply to different underlying data structures.

- Why iterators instead of []s?
	- Good for linked lists. You can keep track of the current position instead of continuously going through the whole list each time you are searching for an element.
	- This is why in c++ you can't access the index for ranged based for loops.

```C++
template<typename T>
void printElems(const T& v) {
	for (typename T::iterator pos = v.begin(); pos != v.end(); pos++) {
		std::cout << *pos << "\n";
	}
}
```
- `++` is redefined to move to the next element. This is different depending upon the underlying data structure.
- You can iterate through different data structures with the same code, allowing templates to be done through compile time instead of run time.

- Removing algorithms using iterators cannot remove. Why?
	- Because all the iterator can do is read and write at a specific location.
	- std::remove gives back the newEnd iterator.
	- std::ranges::subrange{coll.begin(), newEnd}
	- coll | std::views::filter(not3)

### [Constant iterators](#c-data-structures-iterators-and-algorithms)
- `const_iterator` type means you cannot modify the underlying data.
	- `.cbegin()` and `.cend()` is like `.begin()` and `.end()`, but returns a const iterator so you can use `auto`.

### [Different types of iterators](#c-data-structures-iterators-and-algorithms)
- Different types of data structures have iterators which allow for different types of operations. Certain operations are restricted because they aren't performant for the underlying data structure.
	- Contiguous range/iterators(**ContIt**) - All the elements are in continuous memory.
		- Operators:       =, *, ++, ==, !=, --, +=, -=, <, <=, [], -, iterator can be a raw pointer
		- std data types:  vector, array, c-style arrays, strings
	- Random access iterators(**RanIt**) - Data structure where you can jump to and compare with any other position.
		- Operators:       =, *, ++, ==, !=, --, +=, -=, <, <=, [], -
		- std data types:  deque
	- Bidirectional iterators(**BidIt**) - Data structures that only support going forward one or back one.
		- Operators:       =, *, ++, ==, !=, --
		- std data types:  list(linked lsit), associative containers(set, map, etc.)
	- Forward iterators(**FwdIt**) - For data structures that only allow you to go forward.
		- Operators:       =, *, ++, ==, !=
		- std data types:  forward_list(single linked list), unordered containers(hash tables, etc)

	- Input iterators(**InIt**) - Data structures where you can only read the elements once.
		- Operators:       
		- std data types:  istream_iterator
	- Output iterators(**OutIt**) - 

- What are all of the std iterator data structures?

### [back_inserter](#c-data-structures-iterators-and-algorithms)
If you just had an iterator, and you wen to the next element, but you were at the end of the memory, you couldn't insert any more.
The back_insterter automatically does a push_back to expenand the memeory.
- Useful for the transform algorithm

std::back_insert(data structure)

```C++
int square(int in) {
	return in * in;
}

std::list<int> list = {1, 2, 3, 4, 5};
std::vector<int> vec; // empty

// Runtime error because transform writes into unavailable data
std::transform(list.begin(), list.end(),
							 vec.begin(),
							 square)

// Doesn't give an error because back insert automatically extends the size of vec
std::transform(list.begin(), list.end(),
							 std::back_insert(vec),
							 square)
```

## [Algorithms](#c-data-structures-iterators-and-algorithms)
`#include <algorithms>`
- All functions are assumed to be part of the std namespace.

| Usage                            | Description                                                                              |
|----------------------------------|------------------------------------------------------------------------------------------|
| `sort(v.begin(), v.end())`       | Sorts a list in O(nlogn). Tends to use introsort algorithm(quicksort + heap sort)        |
| `sort(v.begin(), v.end(), func)` | You can also sort with a function which takes in 2 args and returns the element you want |
| `stable_sort`                    | Same as `sort`, but equivalent elements are guaranteed to keep the same order            |
| `binary_search(v.begin(), v.end(), search)` | O(logn). Returns true if the value is in the sorted list. |
| `binary_search(v.begin(), v.end(), search, func)` | When list is sorted differently. func can be greater for reverse sorted lists. |
| `lower_bound` | Like binary_search, but returns the first equal to or the next greatest element |
| `upper_bound` | Same, but just gives the next greatest element |
| `reverse()` | O(n) will reverse a list |
| `reverse

- std::find
- std::lower_bound / std::upper_bound
- std::copy
- std::reverse
- std::fill
- std::transform
	- Destination has to be of greater size than the source.
	- Uses a function on each element and puts it into another list
- std::count
- std::remove / std::remove_if
- std::unique
- std::max_element
- std::erase

### [Sort](#c-data-structures-iterators-and-algorithms)
- The data type needs to overload the < operator
- `sort(dataType.begin(), dataType.end())`