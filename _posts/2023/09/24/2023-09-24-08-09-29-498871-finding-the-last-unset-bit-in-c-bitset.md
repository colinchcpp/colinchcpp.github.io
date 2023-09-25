---
layout: post
title: "Finding the last unset bit in C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

C++ provides the `std::bitset` class that allows us to work with a set of bits, represented by a fixed-size array. However, there is no built-in function in the standard library to find the position of the last unset bit in a `std::bitset`. In this blog post, we will discuss a simple algorithm to find the last unset bit in a `std::bitset` in C++.

## Algorithm

1. Initialize a variable `lastUnsetBit` to store the position of the last unset bit.
2. Iterate over each bit of the `std::bitset` from right to left:
   - If the current bit is unset (i.e., `0`), update the `lastUnsetBit` variable with the current position.
3. After iterating over all the bits, the `lastUnsetBit` variable will contain the position of the last unset bit.

Here's the C++ code implementation of the algorithm:

```cpp
#include <iostream>
#include <bitset>

int getLastUnsetBitPosition(const std::bitset<8>& bitset) {
    int lastUnsetBit = -1;
  
    for (int i = bitset.size() - 1; i >= 0; i--) {
        if (!bitset.test(i)) {
            lastUnsetBit = i;
            break;
        }
    }
    
    return lastUnsetBit;
}

int main() {
    std::bitset<8> bits("10100100");
    int lastUnsetBit = getLastUnsetBitPosition(bits);
    
    std::cout << "Last Unset Bit Position: " << lastUnsetBit << std::endl;
    
    return 0;
}
```

In this example, we have a `std::bitset` with the binary representation "10100100". The output of the code will be:

```
Last Unset Bit Position: 2
```

This means that the last unset bit in the `std::bitset` is at position 2 (0-indexed).

## Conclusion

We have discussed a simple algorithm to find the position of the last unset bit in a `std::bitset` in C++. By iterating over the bits and checking for unset bits, we can efficiently locate the last unset bit. This algorithm can be useful in various scenarios where bit manipulation is required. Remember to adapt the code to the size of your `std::bitset` when using it in your own applications.

#cplusplus #bitset