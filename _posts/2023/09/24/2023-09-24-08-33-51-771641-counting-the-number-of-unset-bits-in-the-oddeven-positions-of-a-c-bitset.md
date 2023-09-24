---
layout: post
title: "Counting the number of unset bits in the odd/even positions of a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Bitsets are a useful data structure in C++ that allows efficient manipulation of individual bits. In this blog post, we will explore how to count the number of unset bits in the odd and even positions of a bitset.

## Background

A bitset is a fixed-size sequence of bits, where each bit can be either set (1) or unset (0). The std::bitset class in C++ provides a convenient way to store and manipulate such sequences. 

## Counting Unset Bits in Odd Positions

To count the number of unset bits in the odd positions of a bitset, we can use the bitwise AND operation to mask the even positions and then count the number of unset bits.

Here's an example code snippet:

```cpp
#include <iostream>
#include <bitset>

int countUnsetBitsOdd(const std::bitset<8>& bs) {
    std::bitset<8> oddMask("01010101");
    std::bitset<8> oddBits = bs & oddMask;
    return oddBits.count();
}

int main() {
    std::bitset<8> myBits("10101010");
    int unsetBitsCount = countUnsetBitsOdd(myBits);
    std::cout << "Number of unset bits in odd positions: " << unsetBitsCount << std::endl;
    return 0;
}
```

In the `countUnsetBitsOdd` function, we create a separate bitset `oddMask` with alternating 0s and 1s. We then use the bitwise AND operation (`&`) to apply the mask to the input bitset `bs`, which results in a bitset containing only the bits at odd positions. Finally, we use the `count()` function to count the number of unset bits in the odd positions.

## Counting Unset Bits in Even Positions

Similarly, we can count the number of unset bits in the even positions by masking the odd positions.

Here's an example code snippet:

```cpp
#include <iostream>
#include <bitset>

int countUnsetBitsEven(const std::bitset<8>& bs) {
    std::bitset<8> evenMask("10101010");
    std::bitset<8> evenBits = bs & evenMask;
    return evenBits.count();
}

int main() {
    std::bitset<8> myBits("10101010");
    int unsetBitsCount = countUnsetBitsEven(myBits);
    std::cout << "Number of unset bits in even positions: " << unsetBitsCount << std::endl;
    return 0;
}
```

In the `countUnsetBitsEven` function, we create a separate bitset `evenMask` with alternating 1s and 0s. We then use the bitwise AND operation (`&`) to apply the mask to the input bitset `bs`, which results in a bitset containing only the bits at even positions. Again, we use the `count()` function to count the number of unset bits in the even positions.

## Conclusion

In this blog post, we explored how to count the number of unset bits in the odd and even positions of a bitset in C++. We used bitwise operations and masking techniques to extract the desired positions and then counted the number of unset bits. Bitsets provide a convenient and efficient way to work with individual bits, making them a valuable tool in various applications. 
#programming #C++ #bitwise #bitset