---
layout: post
title: "Finding all occurrences of a specific bit pattern in a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

When working with binary data in C++, the `std::bitset` container provides a convenient way to manipulate and perform operations on sequences of bits. Sometimes, you may need to find all occurrences of a specific bit pattern within a `bitset`. In this blog post, we will explore how to accomplish this task efficiently.

Before we begin, let's assume that you have some experience working with `std::bitset` and understand its basic concepts. If not, it would be helpful to go through the documentation or any tutorial on `std::bitset` before diving into this topic.

## The Problem
Given a `std::bitset` of a certain size and a target bit pattern, the goal is to identify all the positions at which the target pattern occurs within the `bitset`.

## Solution Approach
To solve this problem, we can iterate over the `bitset` bit by bit and compare each possible subsequence with the target pattern. If a match is found, we can store the index where the match begins.

## Example Code
Here's an example code snippet that demonstrates how to find all occurrences of a specific bit pattern in a `std::bitset`:

```cpp
#include <iostream>
#include <bitset>
#include <vector>

std::vector<size_t> findPatternOccurrences(const std::bitset<32>& bitset, const std::bitset<32>& pattern) {
    std::vector<size_t> occurrences;
    size_t patternSize = pattern.size();
    size_t bitsetSize = bitset.size();

    for (size_t i = 0; i <= bitsetSize - patternSize; ++i) {
        if ((bitset >> i) == pattern) {
            occurrences.push_back(i);
        }
    }

    return occurrences;
}

int main() {
    std::bitset<32> bitset(0b11010011010100110101001101010011);
    std::bitset<32> pattern(0b101);

    std::vector<size_t> result = findPatternOccurrences(bitset, pattern);

    if (result.empty()) {
        std::cout << "No occurrences found." << std::endl;
    } else {
        std::cout << "Occurrences found at the following positions: ";
        for (size_t position : result) {
            std::cout << position << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

In this example, we define a function `findPatternOccurrences` that takes in a `bitset` and a `pattern` as parameters. We iterate over the `bitset` using a sliding window of the same size as the `pattern`. If the window matches the `pattern`, we store the starting position in the `occurrences` vector. Finally, we print the positions where the pattern occurred.

## Conclusion
By iterating over a `bitset` and comparing subsequences with a target pattern, we can efficiently find all occurrences of the pattern within the `bitset`. The provided example code demonstrates how to implement this solution in C++.