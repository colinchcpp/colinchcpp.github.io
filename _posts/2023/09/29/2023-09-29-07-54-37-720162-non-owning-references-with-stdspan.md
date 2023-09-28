---
layout: post
title: "Non-owning references with std::span"
description: " "
date: 2023-09-29
tags: [include, include]
comments: true
share: true
---

## What is std::span?

`std::span` is a lightweight, non-owning reference to a contiguous sequence of elements, such as an array, a container, or a buffer. It is defined in the `<span>` header and is part of the C++ Core Guidelines.

Instead of manually managing memory and dealing with pointer arithmetic, `std::span` encapsulates the information about the range of elements it refers to, including the start address, the number of elements, and the size of each element.

## How to use std::span?

To use `std::span`, you need to include the `<span>` header and create an instance of `std::span` by providing the range of elements you want to refer to. Here's a basic example:

```cpp
#include <iostream>
#include <span>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    std::span<int> span(arr, 5);

    for (const auto& element : span) {
        std::cout << element << " ";
    }

    return 0;
}
```

In this example, we create a `std::span` named `span` that references the elements in the `arr` array. We specify `arr` as the starting address and `5` as the number of elements in the range.

We can then treat `span` as if it were a container, using range-based loops or standard algorithms to operate on the elements. `std::span` provides all the necessary methods and iterators to work with the range of elements it refers to.

## Benefits of using std::span

Using `std::span` offers several benefits over raw pointers or iterators:

### 1. Clearer code

By explicitly stating the intent of non-owning references, `std::span` improves the code's readability and maintainability. It clearly communicates that the code does not assume ownership of the data.

### 2. Safety

`std::span` performs bounds checking at runtime, ensuring that you do not access elements outside the range it refers to. This helps prevent bugs caused by out-of-bounds access, leading to safer code.

### 3. Compatibility

`std::span` is designed to work seamlessly with existing code that uses raw pointers or iterators. It can be used as an intermediary type to bridge the gap between legacy code and modern C++.

### 4. Efficiency

`std::span` has no overhead compared to raw pointers or iterators. It simply provides a lightweight wrapper around the range of elements. This makes it efficient both in terms of space and performance.

## Conclusion

`std::span` is a valuable addition to the C++ standard library, providing a safe and efficient way to handle non-owning references to a contiguous sequence of elements. Its introduction in C++20 simplifies code and improves safety when working with ranges. By adopting `std::span`, you can write clearer and more reliable code while enjoying the benefits it brings.

#cpp #stdspan #C++