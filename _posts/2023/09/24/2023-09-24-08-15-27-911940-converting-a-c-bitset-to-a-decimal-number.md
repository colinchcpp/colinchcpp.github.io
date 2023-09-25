---
layout: post
title: "Converting a C++ Bitset to a decimal number"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Bitsets are a useful data structure in C++ that allow you to manipulate individual bits of a binary number. Sometimes, you might need to convert a bitset to a decimal number for further calculations or display purposes. In this blog post, we'll explore how to convert a C++ bitset to a decimal number.

## Converting a Bitset to a Decimal Number

The process of converting a bitset to a decimal number involves iterating through the bitset and calculating the decimal value based on the set bits. Let's take a look at an example:

```cpp
#include <bitset>
#include <iostream>

int main() {
   std::bitset<8> bits("11001010");

   unsigned long decimalValue = 0;
   for (int i = bits.size() - 1; i >= 0; i--) {
      if (bits[i]) {
         decimalValue += (1UL << (bits.size() - 1 - i));
      }
   }

   std::cout << "Decimal value: " << decimalValue << std::endl;

   return 0;
}
```

In the example above, we start by defining a bitset `bits` with a size of 8 and a binary value of "11001010". We then initialize a `decimalValue` variable to store the calculated decimal value. 

Next, we iterate through the bitset from the most significant bit to the least significant bit. For each set bit, we calculate the decimal value by using the left shift operator `<<` and bitwise OR operator `|`. The formula `(1UL << (bits.size() - 1 - i))` calculates the decimal value based on the position of the set bit.

Finally, we print the calculated decimal value to the console.

## Conclusion

Converting a bitset to a decimal number in C++ can be done by iterating through the bitset and calculating the decimal value based on the set bits. With the provided example code, you can now easily convert a bitset to a decimal number in your C++ programs.

#programming #cplusplus