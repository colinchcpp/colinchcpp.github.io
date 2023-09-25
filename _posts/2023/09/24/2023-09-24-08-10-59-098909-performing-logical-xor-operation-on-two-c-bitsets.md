---
layout: post
title: "Performing logical XOR operation on two C++ Bitsets"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---
#include <iostream>
#include <bitset>

int main() {
    // Create two bitsets with the same size
    std::bitset<8> bits1("10101010");
    std::bitset<8> bits2("01010101");
    
    // Perform XOR operation
    std::bitset<8> result = bits1 ^ bits2;
    
    // Print the result
    std::cout << "XOR result: " << result << std::endl;
    
    return 0;
}
```

In the code above, we are performing a logical XOR operation on two C++ bitsets. The `bitset` class in C++ provides a convenient way to manipulate and perform bitwise operations on sets of bits.

First, we create two bitsets `bits1` and `bits2`, with sizes of 8 bits each. We initialize `bits1` with the binary representation of "10101010" and `bits2` with the binary representation of "01010101".

Next, we use the XOR operator (`^`) to perform the XOR operation between `bits1` and `bits2`. The resulting bitset is stored in the `result` variable.

Finally, we print the result using `std::cout`. The output will be the representation of the resulting bitset after performing the XOR operation.

By using bitsets, we can easily perform logical operations on sets of bits in C++. Bitsets are especially useful when dealing with binary data or performing bitwise operations on flags and permissions. #C++ #BitwiseOperations