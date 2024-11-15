[Home](../README.md)

# Programming Tips
C++ is used for all the examples.

<!-- TOC -->

- [Repeatedly ask for user input](#repeatedly-ask-for-user-input)
- [Swapping variables without a temp variable](#swapping-variables-without-a-temp-variable)
- [Getting each digit of an int](#getting-each-digit-of-an-int)
- [Comparing floats](#comparing-floats)
- [Getting random numbers](#getting-random-numbers)
- [Two D arrays](#two-d-arrays)
	- [Convolutional 2d array](#convolutional-2d-array)
- [Rounding with truncation](#rounding-with-truncation)

<!-- /TOC -->

## [Repeatedly ask for user input](#programming-tips)
Ask for user input, validate it, and if it isn't correct ask again.

```C++
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

```C++
// Swap a and b
int a = 50, b = 10;

a = a ^ b;
b = a ^ b;
a = a ^ b;

cout << "a: " << a << endl;
cout << "b: " << b << endl;
```

## [Getting each digit of an int](#programming-tips)

```C++
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
Getting a random integer from a function that generates numbers from 0 to 1.

```C++
int getRandomNum(int start, int end) { // End is exclusive
  return (rand() * (end - start)) + start; // Truncating when converting back into an int
}
```

- `rand() * 10` between 0-9
- `(rand() * 11) + 20` between 20-30

## [Two D arrays](#programming-tips)
`int arr[rows][cols];`

```C++
for (int row = 0; row < arr.size(); row++) {
  for (int col = 0; col < arr[0].size(); col++) {
    auto element = arr[row][col];
  }
}
```

### [Convolutional 2d array](#programming-tips)
- Loop through each element of the 2d array and get it's nearest neighbors.

```C++
void nearestNeighbor(int array[rows][cols], int rIndex, int cIndex) {
  int startCol = cIndex - 1;
  int endCol = startCol + 2;
  if (startCol < 0) startCol = 0;
  if (endCol > cols) endCol = cols;

  int startRow = rIndex - 1;
  int endRow = startRow + 2;
  if (startRow < 0) startRow = 0;
  if (endRow > rows) endRow = rows;

  for (int row = startRow; row < endRow; row++) {
    for (int col = startCol; col < endCol; col++) {
      std::cout << array[row][col] << " ";
    }
  }
}

void convolute(int array[rows][cols], int index) {
  for (int row = 0; row < rows; row++) {
    for (int col = 0; col < cols; col++) {
      nearestNeighbor(array, index);
    }
  }
}
```

## [Rounding with truncation](#programming-tips)
- If you want to round a float number to the nearest int you can add 0.5 and then truncate.
  - `int integer = float + 0.5;`
- If you want to round to the nearest int for negative numbers you can copy the sign before adding 0.5.
  - `int integer = float + std::copysign(0.5, float);`