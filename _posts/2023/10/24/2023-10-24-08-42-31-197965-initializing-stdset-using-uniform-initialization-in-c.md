---
layout: post
title: "Initializing std::set using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, the `std::set` container class from the Standard Library provides an ordered collection of unique elements. When initializing a `std::set`, you can make use of uniform initialization introduced in C++11 to simplify the process.

Uniform initialization allows you to initialize an object by enclosing the initializer values within curly braces `{}`. This syntax is not only concise but also consistent across different types of initialization in C++.

To initialize a `std::set` using uniform initialization, you can follow these steps:

**Step 1:** Include the `<set>` header in your code to gain access to the `std::set` class.

```cpp
#include <set>
```

**Step 2:** Declare a `std::set` object, specifying the type of elements it will store. For example, let's create a set of integers:

```cpp
std::set<int> mySet {1, 3, 2, 5, 4};
```

In the above code, we declare a `std::set<int>` named `mySet` and initialize it with the elements 1, 3, 2, 5, and 4.

That's it! You have now initialized a `std::set` using uniform initialization. The elements will be automatically sorted in ascending order due to the ordered nature of `std::set`.

Here's a complete example showcasing the initialization of a `std::set` using uniform initialization:

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet {1, 3, 2, 5, 4};

    for (const auto& element : mySet) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the above code, we iterate over the elements of `mySet` and print them. The output will be the sorted elements: `1 2 3 4 5`.

Uniform initialization provides a concise and straightforward way to initialize `std::set` containers in C++. It simplifies the code and ensures that the elements are placed in the set while maintaining the order automatically.

By leveraging uniform initialization, you can improve the readability of your code and make it easier to initialize `std::set` objects with initial element values.

## References
- [std::set - C++ Reference](https://en.cppreference.com/w/cpp/container/set)