---
layout: post
title: "Converting binary to decimal using C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Converting a binary number to its decimal equivalent is a common task in programming. In C++, one way to accomplish this is by using the `bitset` class from the standard library. 

The `bitset` class in C++ provides a convenient way to work with binary representations of numbers. It allows you to manipulate individual bits and perform binary operations on them. To convert a binary number to decimal using `bitset`, follow the steps below:

1. Include the `<bitset>` header at the beginning of your C++ program:

```cpp
#include <bitset>
```

2. Declare a `bitset` variable and initialize it with the binary number you want to convert. Make sure the length of the `bitset` is equal to the number of bits in the binary number:

```cpp
std::bitset<8> binaryNumber("10101010");
```

3. Convert the `bitset` to decimal using the `to_ulong()` or `to_ullong()` member function, depending on the size of the `bitset`. These functions return the decimal equivalent of the binary number:

```cpp
unsigned long decimalNumber = binaryNumber.to_ulong();
```

4. Print the result:

```cpp
std::cout << "Decimal Number: " << decimalNumber << std::endl;
```

Here's the complete example code:

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> binaryNumber("10101010");
    unsigned long decimalNumber = binaryNumber.to_ulong();
    
    std::cout << "Decimal Number: " << decimalNumber << std::endl;
    
    return 0;
}
```

When you run the program, the output will be:

```
Decimal Number: 170
```

In this example, we convert the binary number "10101010" to its decimal equivalent using the `bitset` class. The resulting decimal number is 170. You can modify the binary number and experiment with different values to see the conversion in action.

Using the `bitset` class in C++ provides an efficient and straightforward way to convert binary numbers to decimal. It simplifies the process by abstracting the manipulation of individual bits and allows for easy conversion operations.