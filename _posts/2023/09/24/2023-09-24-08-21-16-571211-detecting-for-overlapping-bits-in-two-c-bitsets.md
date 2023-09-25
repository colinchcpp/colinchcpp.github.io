---
layout: post
title: "Detecting for overlapping bits in two C++ Bitsets"
description: " "
date: 2023-09-24
tags: [bitset]
comments: true
share: true
---

Bitsets are a useful data structure in C++ that allow us to efficiently store and manipulate a collection of bits. Sometimes, we may need to determine if two bitsets have overlapping bits, i.e., if any of the bits at the same position in both bitsets are set to 1. In this blog post, we will explore how to detect overlapping bits in two C++ bitsets.

## Required Libraries and Definitions

Before we begin, let's include the necessary library and define the bitset size that we will be working with:

```cpp
#include <bitset>

const int BITSET_SIZE = 32; // Change this as per your requirements
```

## Detecting Overlapping Bits

To detect overlapping bits in two bitsets, we can perform a logical AND operation between the two bitsets and check if the result is non-zero. If the result is non-zero, it means that there is at least one bit position where both bitsets have a 1.

```cpp
bool hasOverlappingBits(const std::bitset<BITSET_SIZE>& bitset1, const std::bitset<BITSET_SIZE>& bitset2) {
    std::bitset<BITSET_SIZE> result = bitset1 & bitset2;
    return result.any();
}
```

In the code snippet above, we define a function `hasOverlappingBits` that takes two bitsets as input and returns a boolean value indicating if there are any overlapping bits. 

The `&` operator performs a logical AND operation between the two bitsets, resulting in a new bitset `result` where each bit is set to 1 if the corresponding bits in both `bitset1` and `bitset2` are 1. The `any()` function checks if any bits in the `result` bitset are set to 1 and returns true if at least one bit is set.

## Usage Example

Let's see how we can use the `hasOverlappingBits` function:

```cpp
int main() {
    std::bitset<BITSET_SIZE> bitset1("10101010");
    std::bitset<BITSET_SIZE> bitset2("11001100");

    bool hasOverlapping = hasOverlappingBits(bitset1, bitset2);
    
    if (hasOverlapping) {
        std::cout << "The bitsets have overlapping bits." << std::endl;
    } else {
        std::cout << "The bitsets do not have overlapping bits." << std::endl;
    }

    return 0;
}
```

In the above example, we create two bitsets `bitset1` and `bitset2` with initial values. We then call the `hasOverlappingBits` function to check if there are any overlapping bits between the two bitsets. Finally, we display a message based on the result.

## Conclusion

Detecting overlapping bits in two C++ bitsets is straightforward with the help of the logical AND operation and the `any()` function provided by the std::bitset class. By applying this technique, we can efficiently determine if there are any bits where two bitsets have a 1 at the same position. This can be useful in various scenarios, such as in bitwise operations or flag checking.

#bitset #C++