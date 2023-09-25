---
layout: post
title: "Shifting bits to the left in C++ Bitset"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In C++, the `<bitset>` library provides a convenient way to manipulate sets of bits. One common operation is shifting the bits to the left, which can be done using the `<<` operator.

Here's an example to demonstrate how to shift bits to the left in C++ using `bitset`:

```cpp
#include <iostream>
#include <bitset>

int main() {
   std::bitset<8> bits(0b00001101); // 8-bit bitset initialized with binary value 00001101

   std::cout << "Before shifting: " << bits << std::endl;

   bits = bits << 2; // Shift the bits to the left by 2 positions

   std::cout << "After shifting: " << bits << std::endl;

   return 0;
}
```

In this example, we initialize an 8-bit `bitset` with the binary value `00001101`. After shifting the bits to the left by two positions using the `<<` operator, the resulting `bitset` becomes `00110100`.

The `<<` operator performs the left shift operation on each bit in the `bitset`. The leftmost bits are shifted out and the rightmost bits are filled with zeros.

The output of the above code will be:

```
Before shifting: 00001101
After shifting: 00110100
```

To compile and run the above code, you'll need a C++ compiler that supports the `<bitset>` library.

Using the shifting operators with `bitset` allows you to perform bitwise operations easily. It's worth noting that shifting bits to the left can also be done with regular integer variables in C++, using the same `<<` operator.

#cpp #bitset #bitshifting