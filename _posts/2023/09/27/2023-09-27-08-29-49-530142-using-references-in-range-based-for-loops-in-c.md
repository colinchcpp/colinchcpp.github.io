---
layout: post
title: "Using references in range-based for loops in C++"
description: " "
date: 2023-09-27
tags: [RangeBasedForLoop]
comments: true
share: true
---

Consider a scenario where you have a vector of integers and you want to square each element. Here's how you can achieve it using references in a range-based for loop:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    for (int& num : numbers) {
        num *= num;
    }

    for(const int& num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, we declare the loop variable `num` as a reference to an `int` using the `&` symbol. By doing so, we can modify the elements of the `numbers` vector directly.

Inside the loop, we square each `num` by multiplying it with itself using the `*=` compound assignment operator.

Finally, we print the modified `numbers` vector to verify that each element has been squared.

Using references in range-based for loops allows us to modify the elements in the container without cloning or creating temporary variables. It provides an efficient and convenient way to perform operations on a container's elements directly.

To summarize, by using references in range-based for loops in C++, we can easily modify elements in a container while iterating over them. This not only enhances readability but also provides a more efficient way of working with containers. #C++ #RangeBasedForLoop