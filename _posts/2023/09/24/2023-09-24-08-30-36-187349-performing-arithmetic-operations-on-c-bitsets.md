---
layout: post
title: "Performing arithmetic operations on C++ Bitsets"
description: " "
date: 2023-09-24
tags: [programming, cplusplus]
comments: true
share: true
---

C++ bitsets are a powerful way to manipulate and perform operations on binary data. They allow you to store and manipulate individual bits as a collection, making it easier to work with binary numbers. One common use case for bitsets is performing arithmetic operations on binary numbers.

In this post, we will explore how to perform arithmetic operations such as addition, subtraction, multiplication, and division on C++ bitsets.

## Addition

To perform addition on two bitsets, we can use the bitwise XOR (^) operation. The XOR operation returns a new bitset with the bits set to 1 where the corresponding bits in the two input bitsets differ.

```cpp
std::bitset<8> bitset1("10101010");
std::bitset<8> bitset2("11001100");

std::bitset<8> sum = bitset1 ^ bitset2;
```

## Subtraction

Subtraction on bitsets can be done using the bitwise AND (&) operation. The AND operation returns a new bitset with the bits set to 1 where the corresponding bits in both input bitsets are 1.

```cpp
std::bitset<8> bitset1("10101010");
std::bitset<8> bitset2("11001100");

std::bitset<8> difference = bitset1 & (~bitset2);
```

## Multiplication

Multiplication on bitsets can be achieved using the bitwise AND (&) and OR (|) operations. The AND operation helps in detecting the common set bits, while the OR operation helps in setting the result bits where any of the corresponding bits in the input bitsets is set.

```cpp
std::bitset<8> bitset1("10101010");
std::bitset<8> bitset2("11001100");

std::bitset<8> product = bitset1 & bitset2;
```

## Division

Division on bitsets can be performed using the XOR (^), AND (&), and NOT (~) operations. The XOR operation helps in detecting the differing bits, while the AND and NOT operations help in determining the quotient bits.

```cpp
std::bitset<8> bitset1("10101010");
std::bitset<8> bitset2("11001100");

std::bitset<8> quotient = bitset1 ^ (bitset1 & bitset2) | (~bitset2);
```

## Conclusion

C++ bitsets provide a convenient way to perform arithmetic operations on binary data. By using bitwise operations, we can manipulate individual bits to perform addition, subtraction, multiplication, and division. This can be particularly useful in scenarios where we need to work with binary numbers.

Remember to familiarize yourself with the bitwise operators such as XOR(^), AND(&), OR(|), and NOT(~) to perform various arithmetic operations on C++ bitsets.

#programming #cplusplus #bitsets #binary #arithmeticoperations