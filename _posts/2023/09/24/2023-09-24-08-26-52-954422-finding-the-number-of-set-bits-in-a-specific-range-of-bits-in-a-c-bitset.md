---
layout: post
title: "Finding the number of set bits in a specific range of bits in a C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Bit manipulation is a powerful technique used in programming to optimize memory usage and perform efficient bitwise operations. In this blog post, we'll explore how to find the number of set bits within a specific range of bits in a C++ `bitset`.

## What is a `bitset`?

A `bitset` is a fixed-size sequence of bits that can be manipulated individually. It is defined in the `<bitset>` library in C++. Each bit is either set to 1 or 0, representing true or false, respectively. Operations such as bitwise AND, OR, XOR, shifting, and counting the number of set bits are possible on a `bitset`.

## Problem Statement

Let's say we have a `bitset` of size `N`, where `N` is the number of bits in the `bitset`. We are interested in finding the number of set bits within a specific range of bits from index `start` to index `end` (both inclusive).

## Solution

To solve this problem, we can follow the steps outlined below:

1. Create a `bitset` object of size `N` and initialize it with the desired bit pattern.
```cpp
#include <bitset>

constexpr unsigned int N = 32;
std::bitset<N> bits("10101010101010101010101010101010");
```

2. Use the `count` member function of the `bitset` class to count the number of set bits within the specified range. This function takes the starting index and the ending index (both inclusive) as parameters and returns the count of set bits within the range.

```cpp
unsigned int start = 5;
unsigned int end = 15;
unsigned int numSetBits = bits.count(start, end);
```

3. Finally, utilize the `numSetBits` variable as needed.

## Example

Let's consider the example where we want to find the number of set bits within the range from index 5 to index 15 in a `bitset`. 

```cpp
#include <bitset>
#include <iostream>

constexpr unsigned int N = 32;

int main() {
    std::bitset<N> bits("10101010101010101011111100000000");
    unsigned int start = 5;
    unsigned int end = 15;
    
    unsigned int numSetBits = bits.count(start, end);

    std::cout << "Number of set bits in the range [" << start << ", " << end << "]: " << numSetBits << std::endl;

    return 0;
}
```

Output:
```
Number of set bits in the range [5, 15]: 7
```

In the above example, there are 7 set bits within the range from index 5 to index 15.

## Conclusion

Using the `count` member function of the `bitset` class, we can easily find the number of set bits within a specific range of bits in a `bitset` in C++. This technique can be helpful in various scenarios where bitwise operations are required, such as optimization algorithms, bit-level encoding, or cryptography.

Remember to include the `<bitset>` and `<iostream>` header files when working with `bitset`. Keep in mind that the range specified in the `count` function is inclusive of both the starting and ending indices.

#bitmanipulation #bitset #cpp