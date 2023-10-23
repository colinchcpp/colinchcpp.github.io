---
layout: post
title: "Initializing std::array using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Here's an example of how to initialize a `std::array` using uniform initialization:

```cpp
#include <array>

int main() {
    std::array<int, 3> numbers = {1, 2, 3};
    return 0;
}
```

In the above code, we declare a `std::array` called `numbers` with a size of 3 and element type of `int`. We then use uniform initialization syntax to initialize the array with the values `{1, 2, 3}`.

Uniform initialization allows us to initialize the `std::array` in a more readable and concise way compared to traditional methods like manually assigning values to each element.

It's important to note that when using uniform initialization, the number of elements in the initializer list must match the size specified in the `std::array` declaration. Otherwise, a compile-time error will occur.

Uniform initialization also works for initializing `std::arrays` of other types, such as `std::string`, `double`, or even user-defined types.

Using uniform initialization with `std::array` simplifies the initialization process and makes the code more readable. It is recommended to use this feature whenever possible to take advantage of the benefits it offers.

For more information, you can refer to the [C++ documentation on std::array](https://en.cppreference.com/w/cpp/container/array).

#cpp #stdarray