---
layout: post
title: "Finding the union of two C++ Bitsets"
description: " "
date: 2023-09-24
tags: [cplusplus, bitsets]
comments: true
share: true
---

To start with, let's create two bitsets, `bitsetA` and `bitsetB`, with some random values:

```cpp
std::bitset<8> bitsetA("10101010");
std::bitset<8> bitsetB("11001100");
```

Now, we want to find the union of these two bitsets. To do this, we can use the bitwise OR operator (`|`). This operator performs a logical OR operation between the bits of the operands, resulting in a new bitset with the bits set to 1 where either of the corresponding bits in the original bitsets is 1.

```cpp
std::bitset<8> unionBitset = bitsetA | bitsetB;
```

Here, `unionBitset` will contain the union of `bitsetA` and `bitsetB`.

To verify the result, we can print the binary representation of the `unionBitset`:

```cpp
std::cout << unionBitset.to_string() << std::endl;
```

This will output `11101110`, which is the binary representation of the union of `bitsetA` and `bitsetB`.

And that's it! You have successfully found the union of two bitsets in C++. You can use this approach with any size of bitsets, as long as they have the same length.

#cplusplus #bitsets