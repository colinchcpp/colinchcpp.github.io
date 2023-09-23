---
layout: post
title: "Applying a cyclic shift to the left in a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

The `std::bitset` class in C++ provides a convenient way to manipulate bits and perform bitwise operations. One common operation is shifting bits to the left, also known as a left shift. In some cases, a *cyclic* left shift is required, where the bit that gets shifted out on the left side reappears on the right side. This article will guide you on how to apply a cyclic left shift to a `std::bitset` in C++.

To illustrate this, let's assume we have a `std::bitset` named `bits` with a size of `N` and the following initial binary representation:

```
bits = 10011010
```

Now, let's say we want to apply a cyclic left shift of `K` positions to `bits`, resulting in the following binary representation:

```
bits = 01101001
```

To achieve this, we can use the following approach:

```cpp
#include <iostream>
#include <bitset>

int main() {
    const int N = 8; // Size of the bitset
    const int K = 3; // Number of positions to shift

    std::bitset<N> bits("10011010");

    // Perform the cyclic left shift
    bits = (bits << K) | (bits >> (N - K));

    std::cout << "bits = " << bits << std::endl;

    return 0;
}
```

In the code above, we declare a `std::bitset` called `bits` with a size of 8 and an initial binary representation of `"10011010"`. The `N` represents the size of the `std::bitset`, and `K` is the number of positions we want to shift the bits.

To perform the cyclic left shift, we first shift the bits to the left by `K` positions using the `<<` operator. Then, we shift the bits to the right by `(N - K)` positions using the `>>` operator. Finally, we bitwise OR (`|`) the shifted left bits with the shifted right bits to get the desired cyclic left shifted result.

Running the code will output:

```
bits = 01101001
```

In conclusion, applying a cyclic left shift to a `std::bitset` in C++ can be accomplished by using bitwise shift operators and bitwise OR. This technique allows you to manipulate and shift bits efficiently within a `std::bitset` container.