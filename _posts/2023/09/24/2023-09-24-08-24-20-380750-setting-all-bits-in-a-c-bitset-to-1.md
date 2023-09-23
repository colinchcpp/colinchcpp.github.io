---
layout: post
title: "Setting all bits in a C++ Bitset to 1"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

To set all the bits in a `bitset` to 1, we can make use of the `set()` member function provided by the `bitset` class. The `set()` function sets all the bits in the `bitset` to 1.

Here is an example code snippet that demonstrates setting all the bits in a `bitset` to 1:

```c++
#include <iostream>
#include <bitset>

int main() {
    const size_t size = 8; // number of bits in the bitset
    std::bitset<size> bitset;

    std::cout << "Before setting: " << bitset << std::endl;
  
    bitset.set(); // set all bits to 1
  
    std::cout << "After setting: " << bitset << std::endl;
  
    return 0;
}
```

In this example, we first define a `bitset` of size 8. We then print the `bitset` before setting all the bits and observe that all bits are initially set to 0. After calling `set()`, all bits in the `bitset` are set to 1. We then print the `bitset` again to verify the change.

When you run the code, you should see the following output:

```
Before setting: 00000000
After setting: 11111111
```

By using the `set()` function of `std::bitset`, we can easily set all the bits in a `bitset` to 1. This can be useful in various scenarios where we need to initialize a bitset with all bits set to a specific value.