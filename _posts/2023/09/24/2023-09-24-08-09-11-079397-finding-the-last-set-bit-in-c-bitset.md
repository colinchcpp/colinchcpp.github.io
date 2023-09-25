---
layout: post
title: "Finding the last set bit in C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with bit manipulation in C++, the `std::bitset` class provides a convenient way to represent and operate on a fixed-size sequence of bits. However, one common task that can be a bit tricky is finding the index of the last set (1) bit in a `bitset`. In this article, we'll explore a simple approach to accomplish this.

## The Problem

Given a `bitset` object, we want to find the index of the rightmost (last) set bit. For example, if the `bitset` has a value of `10101000`, the index of the last set bit is 5.

## The Solution

To find the index of the last set bit in a `bitset`, we can use a bitwise operation called `bsr`, which stands for "bit scan reverse". This operation finds the index of the most significant set bit.

Here is an example code snippet that demonstrates this approach:

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> myBitset("10101000");
    
    // Finding the index of the last set bit
    int lastSetBitIndex = myBitset.size() - 1 - __builtin_clz(myBitset.to_ulong());
    
    std::cout << "Index of the last set bit: " << lastSetBitIndex << std::endl;
    
    return 0;
}
```

In this code, we first create a `bitset` with a value of `10101000`. The `__builtin_clz` function is a built-in C++ function that calculates the number of leading zeros in an integer. We use it to calculate the index of the most significant set bit. By subtracting this index from the size of the `bitset` minus one, we get the index of the last set bit.

## Conclusion

Finding the index of the last set bit in a `bitset` can be accomplished using the `__builtin_clz` function, which calculates the index of the most significant set bit. By subtracting this index from the size of the `bitset` minus one, we can obtain the index of the last set bit. This approach provides an efficient solution to perform this operation.

#C++ #Bitset