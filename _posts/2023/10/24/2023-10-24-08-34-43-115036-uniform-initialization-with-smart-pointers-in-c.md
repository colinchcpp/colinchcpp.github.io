---
layout: post
title: "Uniform initialization with smart pointers in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with smart pointers in C++, it is essential to ensure proper initialization and management of memory resources. One way to achieve this is by using uniform initialization syntax. In this blog post, we will explore how to use uniform initialization with smart pointers to simplify memory management in C++.

## What are smart pointers?

Smart pointers are objects that provide automatic memory management for dynamically allocated resources. They are designed to handle resource deallocation, such as freeing memory, automatically when it is no longer needed. C++ provides three types of smart pointers - `unique_ptr`, `shared_ptr`, and `weak_ptr`, each with their own use cases and ownership semantics.

## Uniform initialization syntax

Uniform initialization syntax allows for a consistent and concise way of initializing objects in C++. It uses curly braces `{}` instead of parentheses `()` or square brackets `[]` for initialization. This syntax can be used with any type, including built-in types, custom-defined types, and smart pointers.

To use uniform initialization with smart pointers, you can simply provide the constructor arguments within curly braces.

## Uniform initialization with `unique_ptr`

The `unique_ptr` provides a single ownership semantics, meaning that it is the sole owner of the dynamically allocated object. Here's an example of using uniform initialization with `unique_ptr`:

```cpp
#include <memory>

int main() {
    // create a unique_ptr using uniform initialization
    auto ptr = std::make_unique<int>(42);

    // access the dynamically allocated object
    std::cout << *ptr << std::endl;

    return 0;
}
```

In the above example, we use uniform initialization to create a `unique_ptr` and initialize it with an `int` value of `42`. The `std::make_unique` function is a convenient way to create a `unique_ptr` and allocate memory in one step.

## Uniform initialization with `shared_ptr`

The `shared_ptr` provides shared ownership semantics, allowing multiple objects to share ownership of the dynamically allocated resource. Here's an example of using uniform initialization with `shared_ptr`:

```cpp
#include <memory>

int main() {
    // create a shared_ptr using uniform initialization
    auto ptr = std::make_shared<int>(42);

    // access the dynamically allocated object
    std::cout << *ptr << std::endl;

    return 0;
}
```

Similarly, we use uniform initialization to create a `shared_ptr` and initialize it with an `int` value of `42`. The `std::make_shared` function is used for creating a `shared_ptr` with memory allocation.

## Benefits of uniform initialization with smart pointers

Using uniform initialization with smart pointers offers several benefits:

- Consistent syntax: Uniform initialization provides a consistent syntax for initializing objects, including smart pointers.
- Readability: The use of curly braces makes the initialization code more readable and easier to understand.
- Avoids confusion: Uniform initialization helps avoid confusion between different kinds of initialization syntax.

## Conclusion

Uniform initialization syntax in C++ provides a convenient and readable way of initializing smart pointers. It simplifies memory management and ensures proper initialization of dynamically allocated resources. By adopting uniform initialization, you can write cleaner and more maintainable code while harnessing the power of smart pointers.

# References
- [C++ Reference - Smart pointers](https://en.cppreference.com/w/cpp/memory)
- [C++ Core Guidelines - Smart pointers](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rr-poly)
- [Bjarne Stroustrup's FAQ on smart pointers](http://www.stroustrup.com/C++11FAQ.html#std-unique-ptr)