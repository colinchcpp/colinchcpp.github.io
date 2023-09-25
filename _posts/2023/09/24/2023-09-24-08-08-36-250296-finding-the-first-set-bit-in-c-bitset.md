---
layout: post
title: "Finding the first set bit in C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with binary data, we often come across situations where we need to find the position of the first set (or '1') bit in a given binary number. In C++, the `bitset` class is a useful tool for working with binary data. In this blog post, we will explore how to efficiently find the position of the first set bit in a `bitset` using bit manipulation techniques.

To begin, let's assume that we have a `bitset` called `binaryNum` with a certain number of bits. We want to find the position of the first set bit in this `bitset`. Here's an example code snippet to illustrate the process:

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> binaryNum("01010100"); // Example binary number

    // Finding the position of the first set bit
    if (binaryNum.any()) {
        int firstSetBitPos = __builtin_ffs(binaryNum.to_ulong()) - 1;
        std::cout << "Position of the first set bit: " << firstSetBitPos << std::endl;
    } else {
        std::cout << "No set bits found." << std::endl;
    }

    return 0;
}
```

In the above code, we create a `bitset` named `binaryNum` with a size of 8 bits and initialize it with the binary number "01010100". The `__builtin_ffs` function is a builtin GCC function that returns the position of the first set bit in an integer. We pass `binaryNum.to_ulong()` to this function to get the position of the first set bit. Note that we subtract 1 from the returned position since `bitset` uses 0-based indexing.

Before finding the first set bit, we use the `any()` function of the `bitset` class to check if any bit is set to '1'. If there are no set bits, we print a message accordingly.

To run the above code, you'll need a GCC compiler that supports the `__builtin_ffs` function. Simply compile and execute the code to see the output.

Remember to include the necessary header files `<iostream>` and `<bitset>` and use the `std` namespace for simplicity in the example code. In practice, it is advisable to avoid using the `using namespace std` directive.

That's it! By using the `bitset` class and the `__builtin_ffs` function, you can efficiently find the position of the first set bit in a `bitset` in C++. Give it a try and see the results for yourself.

#C++ #BitManipulation