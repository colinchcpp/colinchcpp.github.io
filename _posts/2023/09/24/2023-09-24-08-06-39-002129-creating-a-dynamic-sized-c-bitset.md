---
layout: post
title: "Creating a dynamic-sized C++ Bitset"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

A Bitset is a data structure used to implement an array of bits where each bit can be set or cleared individually. In C++, the `std::bitset` class provides a fixed-size implementation of the Bitset. However, if you need a Bitset with a dynamic size, you can create your own implementation using dynamic memory allocation.

## Implementation

Here's an example of a dynamic-sized C++ Bitset class:

```cpp
#include <iostream>
#include <vector>

class DynamicBitset {
private:
    std::vector<bool> bits;

public:
    DynamicBitset() {}

    DynamicBitset(int size) {
        bits.resize(size, false);
    }

    void setBit(int index) {
        bits[index] = true;
    }

    void clearBit(int index) {
        bits[index] = false;
    }

    bool getBit(int index) const {
        return bits[index];
    }
};

int main() {
    DynamicBitset bitset(10);
    bitset.setBit(3);
    bitset.setBit(6);
    bitset.setBit(9);

    std::cout << "Bit at index 3: " << bitset.getBit(3) << std::endl;
    std::cout << "Bit at index 6: " << bitset.getBit(6) << std::endl;
    std::cout << "Bit at index 9: " << bitset.getBit(9) << std::endl;

    return 0;
}
```

In this implementation, we use a `std::vector<bool>` to store the bits dynamically. The `DynamicBitset` class provides methods for setting, clearing, and getting the value of a specific bit.

## Usage

To use the `DynamicBitset` class, you can create an instance by specifying the desired size in the constructor. Then, you can set or clear bits using the `setBit` and `clearBit` methods. To retrieve the value of a bit, you can use the `getBit` method.

## Conclusion

By implementing a dynamic-sized C++ Bitset class, you can have more flexibility in managing bits. This can be useful in various applications such as data compression, algorithm design, and more.

#cplusplus #dynamicbitset