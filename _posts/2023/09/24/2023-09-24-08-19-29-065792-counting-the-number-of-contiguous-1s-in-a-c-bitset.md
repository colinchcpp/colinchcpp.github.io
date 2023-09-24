---
layout: post
title: "Counting the number of contiguous 1s in a C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

The `std::bitset` is a useful class in C++ that allows us to work with a fixed-size sequence of bits. Sometimes, we may come across a situation where we need to count the number of contiguous 1s in a bitset. In this blog post, we will explore how to accomplish this in C++ with a simple example.

Let's consider a scenario where we have a bitset of size 8, and we want to count the number of contiguous 1s in it. Here's how we can do it:

```cpp
#include <iostream>
#include <bitset>

int countContiguousOnes(const std::bitset<8> &bits) {
    int count = 0;
    int maxCount = 0;
    
    for (size_t i = 0; i < bits.size(); i++) {
        if(bits[i]) {
            count++;
            maxCount = std::max(maxCount, count);
        }
        else {
            count = 0;
        }
    }
    
    return maxCount;
}

int main() {
    std::bitset<8> bits("11101111");
    
    int contiguousOnes = countContiguousOnes(bits);
    
    std::cout << "Number of contiguous 1s: " << contiguousOnes << std::endl;
    
    return 0;
}
```

In the code above, we define a function `countContiguousOnes` that takes a reference to a `std::bitset<8>` as input and returns the count of contiguous 1s. We initialize two variables, `count` and `maxCount`, to keep track of the current count of contiguous 1s and the maximum count encountered so far, respectively.

We iterate through each bit in the bitset using a `for` loop. If the bit is set (1), we increment `count` by 1 and update `maxCount` if necessary. If the bit is not set (0), we reset `count` to 0 since the streak of contiguous 1s has ended.

Finally, in the `main` function, we create a `std::bitset<8>` called `bits` initialized with the binary string "11101111". We then call `countContiguousOnes` passing `bits` as the argument and store the result in `contiguousOnes`. We output the result to the console.

By running this code, we will see that the output is `4`, indicating that there are four contiguous 1s in the bitset.

Using a bitset makes it easy to manipulate individual bits and perform bitwise operations efficiently in C++. By counting contiguous 1s, we can gain insights into patterns or analyze binary data more effectively.

#cplusplus #bitset