---
layout: post
title: "Rotating bits in C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Bit manipulation is a fundamental concept in computer programming that involves performing operations on binary digits. One commonly used operation is rotating bits, which involves shifting the bits to the left or right along with wrapping them around.

In C++, the `std::bitset` class from the `<bitset>` library provides a convenient way to manipulate and store binary digits. Let's explore how to rotate bits within a `bitset` using both left and right rotations.

## Left Rotation

To perform a left rotation on a `bitset`, we'll use the bitwise shift operators along with the bitwise OR operator to wrap the bits around.

```cpp
void leftRotate(std::bitset<size>& bits, size_t rotateCount) {
    bits = (bits << rotateCount) | (bits >> (bits.size() - rotateCount));
}
```

In the above code, `bits` is the `bitset` object that we want to rotate, and `rotateCount` specifies the number of positions to rotate the bits to the left. By using the bitwise shift operators, we shift the bits `rotateCount` positions to the left. To wrap the bits around, we perform a bitwise OR between the shifted bits and the bits shifted to the right by `bits.size() - rotateCount`.

## Right Rotation

Performing a right rotation is similar to a left rotation, but we use the bitwise shift operators in the opposite direction along with the bitwise OR operator.

```cpp
void rightRotate(std::bitset<size>& bits, size_t rotateCount) {
    bits = (bits >> rotateCount) | (bits << (bits.size() - rotateCount));
}
```

In the above code, `bits` is the `bitset` object that we want to rotate, and `rotateCount` specifies the number of positions to rotate the bits to the right. We shift the bits `rotateCount` positions to the right using the bitwise shift operators. To wrap the bits around, we perform a bitwise OR between the shifted bits and the bits shifted to the left by `bits.size() - rotateCount`.

## Example Usage

Let's see an example of rotating bits in a `bitset`:

```cpp
#include <bitset>
#include <iostream>

int main() {
    constexpr size_t size = 8;
    std::bitset<size> bits(0b11001110);

    leftRotate(bits, 3);
    std::cout << "Left rotation: " << bits << std::endl;

    rightRotate(bits, 2);
    std::cout << "Right rotation: " << bits << std::endl;

    return 0;
}
```

In the above example, we create a `bitset` with an initial value of `0b11001110`, which is 206 in decimal. After performing a left rotation of 3 positions, the new `bitset` value is `0b01110011`, which is 115 in decimal. Then, we perform a right rotation of 2 positions, resulting in the `bitset` value `0b11001110`, which is the same as the initial value.

By utilizing the bitwise shift operators and the bitwise OR operator, we can easily rotate bits within a `bitset`, enabling efficient manipulation of binary values in C++.

#coding #cplusplus