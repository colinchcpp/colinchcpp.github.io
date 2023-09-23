---
layout: post
title: "Counting set bits in C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

When working with binary data, it can be helpful to count the number of set bits (bits with a value of 1) in a binary representation. In C++, the `std::bitset` class provides a convenient way to work with individual bits.

To count the set bits in a `std::bitset`, we can utilize the `count` member function. Let's take a look at an example:

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> binaryData("11001010");

    int setBitsCount = binaryData.count();

    std::cout << "Number of set bits: " << setBitsCount << std::endl;

    return 0;
}
```

In the example above, we create a `std::bitset` named `binaryData` with a size of 8 bits and initialize it with the binary value `11001010`. We then use the `count` member function to determine the number of set bits in the `bitset`. Finally, we print the result.

The output of this program will be:

```
Number of set bits: 5
```

In this case, there are 5 set bits in the `std::bitset`.

Using the `count` member function of `std::bitset` is a simple and efficient way to count set bits in C++. It provides a clean and readable solution for this common programming task.

#c++ #bit-manipulation