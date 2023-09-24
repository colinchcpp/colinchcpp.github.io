---
layout: post
title: "Applying logical AND between multiple C++ Bitsets"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

To perform a logical AND operation between multiple bitsets, we can use the `&` operator. Here's an example that demonstrates how to do this:

```cpp
#include <bitset>
#include <iostream>

int main() {
  std::bitset<8> bitset1("10101010");
  std::bitset<8> bitset2("01100110");
  std::bitset<8> bitset3("11110000");

  std::bitset<8> result = bitset1 & bitset2 & bitset3;

  std::cout << "Result: " << result << std::endl;

  return 0;
}
```

In the code above, we define three bitsets (`bitset1`, `bitset2`, and `bitset3`) and initialize them with binary strings. We then perform the logical AND operation between these bitsets using the `&` operator and store the result in the `result` variable.

Finally, we print the value of the `result` bitset, which will be the logical AND of all three original bitsets.

The output of the above code will be:

```
Result: 00100000
```

As you can see, the `result` bitset contains the position of the bits that are set to 1 in all three original bitsets.

In summary, applying a logical AND between multiple bitsets in C++ can be easily achieved using the `&` operator. This allows us to perform various bitwise operations efficiently and effectively when working with sets of bits in our code.

#C++ #BitwiseOperators