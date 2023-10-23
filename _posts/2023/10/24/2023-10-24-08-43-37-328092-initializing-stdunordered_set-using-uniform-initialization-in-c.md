---
layout: post
title: "Initializing std::unordered_set using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When initializing an `std::unordered_set`, you can use uniform initialization to provide the initial elements directly. This approach is concise and less error-prone compared to other initialization methods.

Here's an example of how you can initialize an `std::unordered_set` using uniform initialization:

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    // Initialize an unordered_set of integers
    std::unordered_set<int> mySet = {1, 2, 3, 4, 5};

    // Iterate over the set and print the elements
    for (const auto& element : mySet) {
        std::cout << element << " ";
    }

    return 0;
}
```

In the example above, we create an `std::unordered_set` called `mySet` and initialize it with the elements `1`, `2`, `3`, `4`, and `5` using uniform initialization. We then iterate over the set using a range-based for loop and print each element to the standard output.

When you run this code, the output will be:

```
1 2 3 4 5
```

Uniform initialization allows you to provide initial elements directly within the curly braces `{}` when creating an `std::unordered_set` object. This approach can be used with other types as well, such as strings or custom objects.

By using uniform initialization, you can easily initialize an `std::unordered_set` with multiple elements in a concise and readable manner.

References:
- [std::unordered_set - C++ Reference](https://en.cppreference.com/w/cpp/container/unordered_set)
- [Uniform initialization in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/uniform-initialization-in-c/)