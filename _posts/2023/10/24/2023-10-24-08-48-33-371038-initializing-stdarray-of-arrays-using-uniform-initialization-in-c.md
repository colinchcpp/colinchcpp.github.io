---
layout: post
title: "Initializing std::array of arrays using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

To demonstrate this, let's consider an example where we have a `std::array` of two arrays, each containing four integers. We can initialize this `std::array` as follows:

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<std::array<int, 4>, 2> nestedArray = { { {1, 2, 3, 4}, {5, 6, 7, 8} } };

    // Accessing elements of the array
    std::cout << nestedArray[0][2] << std::endl; // Output: 3
    std::cout << nestedArray[1][1] << std::endl; // Output: 6

    return 0;
}
```

In the above code, we first include the necessary headers `<iostream>` and `<array>`. Then, we declare a `std::array` of size 2 of arrays of size 4. We use the uniform initialization syntax to initialize `nestedArray` with two nested arrays.

To access individual elements, we can use the index operator `[]` with the appropriate indices. In this example, we print the values at index `[0][2]` and `[1][1]` using `std::cout`.

By using uniform initialization, we can easily and concisely initialize nested `std::array` structures, improving code readability and maintainability.

References:
- [std::array - cppreference.com](https://en.cppreference.com/w/cpp/container/array)
- [Uniform initialization in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/uniform-initialization-in-c/)