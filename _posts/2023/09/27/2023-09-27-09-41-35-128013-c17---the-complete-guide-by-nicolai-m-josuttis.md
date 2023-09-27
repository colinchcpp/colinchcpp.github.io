---
layout: post
title: ""C++17 - The Complete Guide" by Nicolai M. Josuttis"
description: " "
date: 2023-09-27
tags: [programming]
comments: true
share: true
---

![C++17](https://example.com/c++17-book-cover.jpg)

If you are a C++ developer, you would be thrilled to know that C++17 brings several new features and improvements to the language. To fully grasp these changes and take advantage of them in your code, "C++17 - The Complete Guide" by Nicolai M. Josuttis is an essential resource.

## Overview

"C++17 - The Complete Guide" is a comprehensive book that covers all the major features introduced in C++17. The author, Nicolai M. Josuttis, is a renowned expert in C++ and has extensive experience in teaching and writing about the language. With his expertise, this book offers a thorough and accessible guide to understand and utilize the new capabilities of C++17.

## Key Features

Some of the important features covered in this book include:

1. **Structured Bindings:** Learn how to unpack tuples and other structures into individual variables easily.

2. **`if constexpr` Directives:** Understand how `if constexpr` can be used to conditionally compile code at compile-time.

3. **`constexpr` Lambda Functions:** Discover how to define and use lambda functions in constant expressions.

4. **Fold Expressions:** Learn how to combine variadic template parameters in a fold-like fashion.

## Example Code

Here's an example of how C++17's structured bindings make code more concise and readable:

```cpp
#include <tuple>

int main() {
    std::tuple<int, std::string, double> person(42, "John Doe", 3.14);

    auto [age, name, pi] = person; // Structured binding declaration

    // Use the individual variables
    std::cout << name << " is " << age << " years old. Pi is approximately " << pi << std::endl;

    return 0;
}
```

## Conclusion

"C++17 - The Complete Guide" by Nicolai M. Josuttis is a must-have resource for any C++ developer who wants to stay up to date with the latest features and improvements in the language. Whether you are a beginner or an experienced programmer, this book will help you harness the power of C++17 and write more efficient and expressive code.

Grab a copy of "C++17 - The Complete Guide" and unlock the full potential of C++17 today!

#C++ #programming