---
layout: post
title: "Finding the symmetric difference between two C++ Bitsets"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

To find the symmetric difference between two `bitset` objects in C++, you can use the bitwise XOR operator (`^`). The XOR operator compares the corresponding bits between the two bitsets and sets the result bit to 1 if the bits are different, and 0 otherwise.

Here's an example code that demonstrates finding the symmetric difference between two `bitset` objects:

```cpp
#include <iostream>
#include <bitset>

int main() {
  std::bitset<8> bitset1("01100110");    // First bitset
  std::bitset<8> bitset2("11001100");    // Second bitset

  std::bitset<8> symmetricDiff = bitset1 ^ bitset2;

  std::cout << "Symmetric Difference: " << symmetricDiff << std::endl;

  return 0;
}
```

In this example, we have two `bitset` objects, `bitset1` and `bitset2`, each containing 8 bits. We initialize them with binary values using the constructor that takes a string of 0s and 1s. 

Then, we use the XOR operator (`^`) to calculate the symmetric difference between `bitset1` and `bitset2` and store the result in the `symmetricDiff` variable.

Finally, we print the resulting symmetric difference using the `cout` statement.

When you run this code, you should see the following output:

```
Symmetric Difference: 10101010
```

Remember, the output is a new `bitset` object that represents the bits that are different between the two input bitsets.

By utilizing the power of the `bitset` class and the XOR operator, you can easily find the symmetric difference between two bitsets in C++. Give it a try and see how it can simplify your bit manipulation tasks!

#C++ #BitwiseOperations