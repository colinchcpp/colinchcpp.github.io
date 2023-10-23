---
layout: post
title: "Initializing std::array of std::std::arrays using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

`std::array` is a container introduced in the C++ standard library that provides a fixed-size, array-like structure with a friendly interface. Let's see how we can use it to initialize a multidimensional array.

First, we need to include the `<array>` header:

```cpp
#include <array>
```

Next, we can define a multidimensional array of `std::array` using uniform initialization syntax. Here's an example of initializing a 2x2 multidimensional array:

```cpp
std::array<std::array<int, 2>, 2> myArray = { { {1, 2}, {3, 4} } };
```

In this example, `myArray` is an array of arrays. Each element of `myArray` is an `std::array<int, 2>`, representing a row in the multidimensional array.

We use double braces `{{ ... }}` to initialize `myArray`. The outer braces represent the outermost array, and the inner braces represent each inner array (row).

Finally, we provide the values to initialize the multidimensional array. In the above example, we initialize it with the values `{1, 2}` and `{3, 4}`.

You can access and manipulate individual elements of the multidimensional array using the usual notation, for example:

```cpp
int element = myArray[0][1]; // Accessing the element at position (0, 1)
myArray[1][0] = 5; // Modifying the element at position (1, 0)
```

Using `std::array` and uniform initialization provides a concise and readable way to initialize and work with multidimensional arrays in C++. It helps ensure type safety and eliminates the hassle of manual initialization.

References:
- [std::array - cppreference.com](https://en.cppreference.com/w/cpp/container/array)
- [Uniform initialization - cppreference.com](https://en.cppreference.com/w/cpp/language/list_initialization)
- [Multidimensional arrays - cplusplus.com](http://www.cplusplus.com/doc/tutorial/arrays/)