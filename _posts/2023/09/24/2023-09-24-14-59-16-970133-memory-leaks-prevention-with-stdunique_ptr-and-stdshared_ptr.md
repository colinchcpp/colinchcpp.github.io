---
layout: post
title: "Memory leaks prevention with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Memory leaks are a common issue in software development, especially when dealing with dynamic memory allocation. They occur when allocated memory is not properly deallocated, leading to a loss of memory resources over time. This can result in degraded performance and possible crashes.

To prevent memory leaks in C++, the standard library provides smart pointers like `std::unique_ptr` and `std::shared_ptr`. These smart pointers offer automated memory management by ensuring that allocated resources are properly released when no longer needed.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that manages a dynamically allocated object and takes ownership of it. It ensures that the object is deleted when the `std::unique_ptr` goes out of scope. Let's see an example:

```cpp
#include <memory>

void foo()
{
    std::unique_ptr<int> p(new int(10));
    // Do something with p
} // p is automatically deleted here

int main()
{
    foo();
    // Rest of the code
}
```

In the above example, the memory allocated for `int` is automatically deallocated when `std::unique_ptr` `p` goes out of scope. This helps in preventing memory leaks as the responsibility of deallocating the memory is automatically handled.

## `std::shared_ptr`

While `std::unique_ptr` provides exclusive ownership of the allocated resource, `std::shared_ptr` allows multiple pointers to refer to the same resource. It keeps track of all the objects sharing ownership and deletes the resource only when the last `std::shared_ptr` referencing it goes out of scope.

```cpp
#include <memory>

void foo()
{
    std::shared_ptr<int> p1(new int(10));
    std::shared_ptr<int> p2 = p1; // Shared ownership

    // Do something with p1 and p2

} // p1 and p2 are deleted here

int main()
{
    foo();
    // Rest of the code
}
```

In the above example, both `p1` and `p2` are `std::shared_ptr` objects sharing ownership of the dynamically allocated `int`. The resource is automatically deallocated when both `std::shared_ptr` objects go out of scope. This prevents memory leaks by handling deallocation for all shared pointers correctly.

## Conclusion

Memory leaks can be a significant problem in software development. However, by utilizing smart pointers like `std::unique_ptr` and `std::shared_ptr` from the C++ standard library, you can greatly reduce the risk of memory leaks. These smart pointers provide automatic memory management, ensuring that dynamically allocated resources are correctly deallocated when they are no longer needed. By incorporating these smart pointers into your code, you can improve the overall stability and performance of your applications.

#cpp #memorymanagement #smartpointers