---
layout: post
title: "Finding the intersection of two C++ Bitsets"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

To find the intersection of two bitsets, we can use the bitwise AND operator. This operator performs a logical AND operation on each corresponding pair of bits from the two bitsets. The result is a new bitset where each bit is set to 1 if both corresponding bits in the input bitsets are also 1.

Let's take a look at an example:

```cpp
#include <iostream>
#include <bitset>

int main() {
  std::bitset<8> bitset1("10101010");
  std::bitset<8> bitset2("11001100");

  std::bitset<8> intersection = bitset1 & bitset2;

  std::cout << "Intersection: " << intersection << std::endl;

  return 0;
}
```

In this example, we have two bitsets: `bitset1` and `bitset2` with 8 bits each. We have initialized `bitset1` with the binary value "10101010" and `bitset2` with "11001100". 

We then use the bitwise AND operator (`&`) to find the intersection of `bitset1` and `bitset2`. The resulting bitset `intersection` will contain 1s only in the positions where both `bitset1` and `bitset2` have 1s.

When we run this code, the output will be:

```
Intersection: 10001000
```

In this case, the intersection of `bitset1` and `bitset2` is "10001000".

By utilizing the bitwise AND operator, we can easily find the common bits between two bitsets. This approach can be extended to perform other set operations, such as union and difference, using different bitwise operators.

So, the next time you need to find the intersection of two C++ bitsets, give the bitwise AND operator a try. It's a simple and efficient way to accomplish this task.

#cplusplus #bitsets