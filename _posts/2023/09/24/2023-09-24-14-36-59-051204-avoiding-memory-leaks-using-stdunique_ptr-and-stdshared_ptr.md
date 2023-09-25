---
layout: post
title: "Avoiding memory leaks using `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Memory leaks are a common problem in software development, especially when dealing with low-level languages like C++. A memory leak occurs when allocated memory is not properly deallocated, leading to memory consumption steadily increasing over time. This can eventually cause the application to crash or run out of memory.

Fortunately, C++ provides smart pointers that can help us avoid memory leaks. Two of the most commonly used smart pointers are `std::unique_ptr` and `std::shared_ptr`. In this article, we will explore how these smart pointers work and how to utilize them to prevent memory leaks in our code.

## `std::unique_ptr`

The `std::unique_ptr` is a smart pointer that owns and manages a dynamically allocated object. It guarantees that only one `std::unique_ptr` instance can own the resource at a time. When the owning `std::unique_ptr` goes out of scope, it automatically deletes the managed object, ensuring proper cleanup of the allocated memory.

Here's an example that demonstrates the usage of `std::unique_ptr`:

```cpp
#include <memory>

void exampleFunction()
{
    std::unique_ptr<int> myUniquePtr = std::make_unique<int>(42);
    // Use myUniquePtr as needed
} // myUniquePtr is automatically deleted here
```

In the example above, we create a `std::unique_ptr` named `myUniquePtr` that owns an integer with the value of 42. When `exampleFunction()` completes, the `std::unique_ptr` gets destroyed, and the allocated integer is automatically deleted.

## `std::shared_ptr`

While `std::unique_ptr` enforces exclusive ownership of the resource, `std::shared_ptr` allows multiple smart pointers to share ownership of the same resource. It keeps track of the number of `std::shared_ptr` instances that point to a particular object and deletes the object only when the last `std::shared_ptr` goes out of scope.

Let's look at an example to understand how `std::shared_ptr` works:

```cpp
#include <memory>

void exampleFunction()
{
    std::shared_ptr<int> mySharedPtr = std::make_shared<int>(42);
    std::shared_ptr<int> anotherSharedPtr = mySharedPtr;
    // Use mySharedPtr and anotherSharedPtr as needed
} // both mySharedPtr and anotherSharedPtr are automatically deleted here
```

In this example, we create a `std::shared_ptr` named `mySharedPtr` that owns an integer with the value of 42. We then create another `std::shared_ptr` named `anotherSharedPtr` and assign it the value of `mySharedPtr`. Both smart pointers now share ownership of the same integer resource. When `exampleFunction()` completes, both `std::shared_ptr` instances are destroyed, and the allocated integer is deleted only once.

## Conclusion

Memory leaks can be detrimental to software performance and stability. Using smart pointers like `std::unique_ptr` and `std::shared_ptr` in C++ can help us avoid memory leaks by automatically managing the lifetime of dynamically allocated objects. By using these smart pointers correctly, we can ensure that memory is deallocated correctly, reducing the risk of memory leaks in our code.

#C++ #MemoryManagement