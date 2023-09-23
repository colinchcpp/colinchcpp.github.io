---
layout: post
title: "Bitwise operations in C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, cplusplus]
comments: true
share: true
---

Bitwise operations are fundamental operations in computer programming that manipulate individual bits within binary numbers. These operations are commonly used in scenarios where we need to perform low-level optimizations or work with binary data. In this article, we will explore bitwise operations using the C++ `bitset` class.

The `bitset` is a powerful class in C++ that provides a high-level interface to manipulate and operate on a fixed number of bits. It encapsulates an array of bits and provides various member functions to perform bitwise operations.

## Creating a `bitset`

To start using the `bitset` class, you first need to include the `<bitset>` header. Then, you can create a `bitset` object by specifying the number of bits it should store.

```cpp
#include <bitset>

constexpr int BITS_COUNT = 8;
std::bitset<BITS_COUNT> bits;
```

In the above example, we create a `bitset` object called `bits` with 8 bits. This will create a `bitset` that can hold 8 binary digits.

## Setting and Accessing Bits

Once you have a `bitset`, you can set and access individual bits using the `[]` operator.

```cpp
bits[0] = 1; // Set the first bit to 1
bits[3] = 0; // Set the fourth bit to 0

bool firstBit = bits[0]; // Access the first bit
```

In the above code snippet, we set the first bit of `bits` to 1 and the fourth bit to 0. We also access the value of the first bit and store it in the `firstBit` variable.

## Bitwise Operations

The `bitset` class provides a set of member functions to perform bitwise operations.

### AND Operation

To perform the logical AND operation between two `bitset` objects, we can use the `&` operator or the `and` member function.

```cpp
std::bitset<BITS_COUNT> bits1("01010101");
std::bitset<BITS_COUNT> bits2("00110011");
std::bitset<BITS_COUNT> result = bits1 & bits2;
```

In the above code, we perform the AND operation between `bits1` and `bits2` and store the result in the `result` `bitset` object.

### OR Operation

To perform the logical OR operation between two `bitset` objects, we can use the `|` operator or the `or` member function.

```cpp
std::bitset<BITS_COUNT> bits1("01010101");
std::bitset<BITS_COUNT> bits2("00110011");
std::bitset<BITS_COUNT> result = bits1 | bits2;
```

In the above code, we perform the OR operation between `bits1` and `bits2` and store the result in the `result` `bitset` object.

### XOR Operation

To perform the logical XOR operation between two `bitset` objects, we can use the `^` operator or the `xor` member function.

```cpp
std::bitset<BITS_COUNT> bits1("01010101");
std::bitset<BITS_COUNT> bits2("00110011");
std::bitset<BITS_COUNT> result = bits1 ^ bits2;
```

In the above code, we perform the XOR operation between `bits1` and `bits2` and store the result in the `result` `bitset` object.

## Conclusion

Bitwise operations with the C++ `bitset` class provide a convenient way to manipulate bits at a low level. Whether you need to perform logical operations or bitwise manipulations, the `bitset` class offers an efficient and easy-to-use interface.

Understanding bitwise operations is crucial in optimizing algorithms, working with binary data, and implementing various data structures. By leveraging the power of `bitset`, you can simplify your code and take advantage of the low-level bit manipulation capabilities provided by the C++ language.

#cplusplus #bitwiseoperations