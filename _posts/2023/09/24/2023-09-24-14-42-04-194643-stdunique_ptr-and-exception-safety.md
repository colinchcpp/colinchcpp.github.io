---
layout: post
title: "`std::unique_ptr` and exception safety"
description: " "
date: 2023-09-24
tags: [include, smartpointers]
comments: true
share: true
---

In C++, exception safety is a crucial aspect of writing robust and reliable code. When exceptions are thrown, it is important to ensure that resources are properly managed and no memory leaks occur. 

One powerful tool in the C++ Standard Library for managing resource acquisition and release is `std::unique_ptr`. This smart pointer provides exclusive ownership of an object and automatically deallocates the resource when it goes out of scope.

The use of `std::unique_ptr` greatly enhances exception safety as it guarantees that the owned resource will be properly cleaned up, whether an exception is thrown or not. Let's take a look at how it can be used to achieve exception-safe code.

## Basic Usage

To create a `std::unique_ptr`, you can use the `std::make_unique` function (C++14 and above) or directly initialize it with a raw pointer. Here's an example of both methods:

```cpp
#include <memory>

void foo()
{
    // Using std::make_unique
    std::unique_ptr<int> ptr1 = std::make_unique<int>(42);
    
    // Using direct initialization
    std::unique_ptr<int> ptr2(new int(42));
    
    // Use ptr1 and ptr2 as needed...
}
```

In this example, two `std::unique_ptr` objects are created, `ptr1` and `ptr2`, both owning an `int` with value 42.

## Exception Safety

One of the key features of `std::unique_ptr` is its ability to handle exceptions while providing exception safety. When an exception is thrown, the normal program flow is disrupted, but `std::unique_ptr` guarantees that the owned resource will be deallocated correctly.

Consider the following function that demonstrates exception safety using `std::unique_ptr`:

```cpp
void bar()
{
    std::unique_ptr<int> ptr(new int(10));
    
    // Perform some operations that might throw exceptions
    // ...
    
    // If an exception is thrown, the owned resource is deallocated automatically
}
```

In this example, if an exception is thrown during the operations inside the `bar` function, the `std::unique_ptr` will automatically call the destructor of the owned object, deallocating the memory.

## Conclusion

`std::unique_ptr` is a powerful tool in C++ for managing resources and achieving exception safety. By utilizing `std::unique_ptr`, you ensure that resources are properly cleaned up, even in the presence of exceptions.

Remember, when writing C++ code, it is essential to consider exception safety to avoid leaks and maintain the integrity and reliability of your software.

#cpp #smartpointers #exceptionhandling