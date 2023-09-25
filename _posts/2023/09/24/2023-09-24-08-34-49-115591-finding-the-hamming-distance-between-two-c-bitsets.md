---
layout: post
title: "Finding the hamming distance between two C++ Bitsets"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

When working with binary data, it is often useful to calculate the Hamming distance between two bitsets. The Hamming distance measures the number of positions at which the corresponding bits between two bitsets are different. In this blog post, we will explore how to find the Hamming distance between two C++ `bitset` objects.

## Initializing Bitsets

First, let's start by initializing two `bitset` objects. We will assume that both bitsets have the same size.

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> a("10101010");
    std::bitset<8> b("11110000");

    std::cout << "Bitset a: " << a << std::endl;
    std::cout << "Bitset b: " << b << std::endl;

    return 0;
}
```

In this example, we have initialized two `bitset` objects, `a` and `b`, with binary strings "10101010" and "11110000" respectively. The size of both bitsets has been set to 8 using template argument `<8>`. We print the values of both bitsets for verification purposes.

## Calculating the Hamming Distance

To calculate the Hamming distance between two bitsets, we can use the bit-wise XOR operator (`^`) to find the positions where the bits differ. Then, by counting the number of set bits in the result, we can determine the Hamming distance.

Here's the code to calculate the Hamming distance:

```cpp
int hammingDistance(std::bitset<8> a, std::bitset<8> b) {
    std::bitset<8> diff = a ^ b;
    int distance = diff.count();
    return distance;
}

int main() {
    std::bitset<8> a("10101010");
    std::bitset<8> b("11110000");

    int distance = hammingDistance(a, b);
    std::cout << "Hamming Distance: " << distance << std::endl;

    return 0;
}
```

In this code, we define a function `hammingDistance` that takes two `bitset` objects as input. We calculate the difference between the two bitsets using the XOR operator (`^`) and store the result in the `diff` variable. We then use the `count` function to count the number of set bits in the `diff` bitset and return the count as the Hamming distance.

Finally, we call the `hammingDistance` function with `a` and `b` and print the resulting Hamming distance.

## Conclusion

Calculating the Hamming distance between two C++ `bitset` objects is a straightforward process using the bit-wise XOR operator and the `count` function. This can be useful in various scenarios where you need to measure the difference between binary data.

#bitsets #C++