---
layout: post
title: "Applying bit operations on non-contiguous bits in a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Bit manipulation is a powerful technique in programming, especially when working with low-level operations or optimizing code. The C++ Standard Library provides the `std::bitset` class, which is a convenient wrapper to manipulate sequences of bits. However, by default, the `std::bitset` class assumes that the bits are contiguous. But what if we want to perform bit operations on non-contiguous bits? In this blog post, we will explore how to achieve this in C++ using `std::bitset`.

### The Problem

Let's say we have a `std::bitset` of size 8, and we want to perform bit operations on bits at indices 1, 3, and 6. By default, `std::bitset` does not provide a direct way to perform operations on non-contiguous bits.

### The Solution

To manipulate non-contiguous bits, we can use the logical bitwise operators (`&`, `|`, `^`) in conjunction with the `std::bitset::test()` and `std::bitset::set()` functions.

Here's an example code snippet to demonstrate how to perform bit operations on non-contiguous bits using `std::bitset`:

```cpp
#include <bitset>
#include <iostream>

int main() {
    std::bitset<8> bitset;

    // Set the bits at indices 1, 3, and 6
    bitset.set(1);
    bitset.set(3);
    bitset.set(6);

    // Perform bit operations on the non-contiguous bits
    std::bitset<8> operationResult = (bitset.test(1) & bitset.test(3)) | bitset.test(6);

    std::cout << "Result: " << operationResult << std::endl;

    return 0;
}
```

In the above code, we create a `std::bitset` of size 8 and set the bits at indices 1, 3, and 6 using `std::bitset::set()`. Then, we perform bit operations on these non-contiguous bits using the logical bitwise operators. Finally, we print the result to the console.

### Conclusion

Although the `std::bitset` class in C++ assumes contiguous bits by default, we can still perform bit operations on non-contiguous bits by combining logical bitwise operators with `std::bitset::test()` and `std::bitset::set()`. By leveraging these techniques, we can manipulate specific bits in a `std::bitset` without the constraint of contiguity.

#bitmanipulation #bitset #cplusplus