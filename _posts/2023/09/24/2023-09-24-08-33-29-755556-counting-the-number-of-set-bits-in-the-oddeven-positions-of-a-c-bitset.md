---
layout: post
title: "Counting the number of set bits in the odd/even positions of a C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Let's consider a scenario where we have a `bitset` containing a binary representation of a number. Our goal is to count the number of set bits (1s) in the odd and even positions separately.

To begin, let's assume that our `bitset` has a fixed size of 8 bits. We can define the `bitset` and initialize it with a binary number as follows:

```cpp
#include <bitset>
#include <iostream>

int main() {
    std::bitset<8> bits("10101010");
    std::cout << "Original bitset: " << bits << std::endl;

    return 0;
}
```

In the above code, we have defined a `bitset` object called `bits` with a size of 8 bits. We initialized it with the binary number "10101010". We have also included the necessary headers for using `bitset` and `iostream` in C++.

To count the number of set bits in the odd positions, we can use bit shifting and bitwise AND operations. Here's the code to accomplish that:

```cpp
#include <bitset>
#include <iostream>

int countSetBitsOdd(std::bitset<8> bits) {
    // Shift the bits right by 1 position
    bits >>= 1;

    // Perform bitwise AND with a mask to count set bits in odd positions
    bits &= std::bitset<8>("01010101");

    // Count the number of set bits
    return bits.count();
}

int main() {
    std::bitset<8> bits("10101010");
    std::cout << "Original bitset: " << bits << std::endl;

    int setBitsOdd = countSetBitsOdd(bits);
    std::cout << "Number of set bits in odd positions: " << setBitsOdd << std::endl;

    return 0;
}
```

In the `countSetBitsOdd` function, we first shift the bits right by 1 position using the `>>=` operator. This effectively moves all the bits one position to the right. Then, we perform a bitwise AND operation with a mask `01010101`, which isolates the bits in odd positions. Finally, we use the `count` function of the `bitset` class to count the number of set bits.

Similarly, we can count the number of set bits in the even positions using the following code:

```cpp
#include <bitset>
#include <iostream>

int countSetBitsEven(std::bitset<8> bits) {
    // Perform bitwise AND with a mask to count set bits in even positions
    bits &= std::bitset<8>("10101010");

    // Count the number of set bits
    return bits.count();
}

int main() {
    std::bitset<8> bits("10101010");
    std::cout << "Original bitset: " << bits << std::endl;

    int setBitsEven = countSetBitsEven(bits);
    std::cout << "Number of set bits in even positions: " << setBitsEven << std::endl;

    return 0;
}
```

In the `countSetBitsEven` function, we directly perform a bitwise AND operation with a mask `10101010`, isolating the bits in even positions.

By using the above code snippets, you will be able to count the number of set bits in both odd and even positions of a C++ `bitset`.

#C++ #BitManipulation