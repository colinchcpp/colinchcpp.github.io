---
layout: post
title: "Applying logical OR between multiple C++ Bitsets"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Let's first start by creating two Bitsets and applying the logical OR operation between them:

```cpp
#include <bitset>
#include <iostream>

int main() {
  std::bitset<8> bitset1("00001111");
  std::bitset<8> bitset2("11110000");

  std::bitset<8> result = bitset1 | bitset2;

  std::cout << "Result: " << result << std::endl;

  return 0;
}
```

In the above code, we have defined two Bitsets, `bitset1` and `bitset2`, with a size of 8 bits each. We have initialized them with binary values `00001111` and `11110000` respectively. The logical OR operation (`|`) is performed between `bitset1` and `bitset2`, and the result is stored in the `result` Bitset.

To print the result, we use `std::cout` and the `<<` operator to output the value of `result` to the console.

When you run the code, the output will be:
```
Result: 11111111
```

As you can see, the logical OR operation between `bitset1` and `bitset2` combines the set bits from both Bitsets, resulting in all bits being set (`11111111`).

Now, let's explore how to apply logical OR between multiple Bitsets dynamically. We can achieve this by using a loop and performing the logical OR operation iteratively:

```cpp
#include <bitset>
#include <iostream>
#include <vector>

int main() {
  std::vector<std::bitset<8>> bitsets = {std::bitset<8>("00001111"),
                                         std::bitset<8>("11110000"),
                                         std::bitset<8>("01010101")};

  std::bitset<8> result;

  for (const std::bitset<8>& bitset : bitsets) {
    result |= bitset;
  }

  std::cout << "Result: " << result << std::endl;

  return 0;
}
```

In the updated code, we have defined a `std::vector` of Bitsets named `bitsets`, which contains three Bitsets initialized with different binary values. We have also defined an empty `result` Bitset to store the cumulative result of the logical OR operation.

Using a range-based for loop, we iterate through each Bitset in `bitsets` and perform the logical OR operation (`|`) with the `result` Bitset. The result is accumulated in `result` as we iterate through the Bitsets.

Finally, we print the `result` using `std::cout` and the `<<` operator.

Running the updated code will give the following output:
```
Result: 11111111
```

As you can see, the logical OR operation is applied iteratively to all Bitsets in the `bitsets` vector, resulting in the same output as before.

In conclusion, applying logical OR between multiple C++ Bitsets is straightforward. By using the `|` operator, you can combine individual bits from multiple Bitsets into a final result. Whether you are performing the operation between two or multiple Bitsets, you can leverage the power and efficiency of Bitsets to manipulate bits at a granular level.