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

<!-- /TOC -->

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
Getting a random number from a function that generates numbers from 0-1.

```c++
int getRandomNum(int start, int end) { // Both are inclusive
  return (rand() % (end - start + 1)) + start;
}
```

- `rand() % 10` between 0-9
- `(rand() % 11) + 20` between 20-30

## [Two D arrays](#programming-tips)
`int arr[rows][cols];`

```C++
for (int row = 0; row < arr.size(); row++) {
  for (int col = 0; col < arr[0].size(); col++) {
    auto element = arr[row][col];
  }
}
```