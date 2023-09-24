---
layout: post
title: "Applying bitwise operations on different portions of a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

## Initializing a Bitset

First, let's initialize a bitset with a given size and set some of its bits to 1. We can use the `std::bitset` class provided by the C++ standard library.

```cpp
#include <bitset>

int main() {
    // Create a bitset of size 8
    std::bitset<8> myBitset;

    // Set some bits to 1
    myBitset.set(0);  // Set the first bit to 1
    myBitset.set(3);  // Set the fourth bit to 1
    myBitset.set(5);  // Set the sixth bit to 1

    return 0;
}
```

## Extracting Bits from a Bitset

To extract a specific portion of bits from a bitset, we can use the `std::bitset` member function `to_ulong()` or `to_ullong()` depending on the size of the bitset.

```cpp
#include <bitset>

int main() {
    // Create a bitset of size 8
    std::bitset<8> myBitset;

    // Set some bits to 1
    myBitset.set(0);  // Set the first bit to 1
    myBitset.set(3);  // Set the fourth bit to 1
    myBitset.set(5);  // Set the sixth bit to 1

    // Extract the first 4 bits as an integer
    unsigned int extractedBits = myBitset.to_ulong();

    return 0;
}
```

## Setting Bits in a Bitset

To set specific bits in a bitset to a certain value, we can use the `std::bitset` member function `set()`.

```cpp
#include <bitset>

int main() {
    // Create a bitset of size 8
    std::bitset<8> myBitset;

    // Set some bits to 1
    myBitset.set(0);  // Set the first bit to 1
    myBitset.set(3);  // Set the fourth bit to 1
    myBitset.set(5);  // Set the sixth bit to 1

    // Set the second bit to 1
    myBitset.set(1, true);

    // Set the fifth bit to 0
    myBitset.set(4, false);

    return 0;
}
```

## Conclusion

In this blog post, we have seen how to apply bitwise operations on different portions of a C++ bitset. We learned how to initialize a bitset, extract bits from a bitset, and set bits in a bitset. Bitsets provide a convenient way to work with sets of bits, allowing us to perform low-level operations efficiently.

#C++ #Bitset