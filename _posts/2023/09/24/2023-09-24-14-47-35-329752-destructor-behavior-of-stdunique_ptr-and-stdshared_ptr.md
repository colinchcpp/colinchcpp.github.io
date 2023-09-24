---
layout: post
title: "Destructor behavior of `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [programming, Cplusplus]
comments: true
share: true
---

When working with dynamically allocated resources in C++, it is crucial to manage memory properly to avoid memory leaks and other issues. Two smart pointer classes provided by the C++ Standard Library, `std::unique_ptr` and `std::shared_ptr`, are widely used for efficient memory management.

Both `std::unique_ptr` and `std::shared_ptr` have different destructor behaviors, which impact how they handle the release of allocated memory.

## `std::unique_ptr`

`std::unique_ptr` is a "unique" smart pointer that ensures exclusive ownership of the resource it manages. It is move-only and guarantees that there will be only one `std::unique_ptr` instance pointing to the resource at any given time. When the `std::unique_ptr` goes out of scope or is explicitly reset, its destructor is called.

The destructor of `std::unique_ptr` releases the associated memory by calling the delete operator on the managed pointer. This ensures that the allocated memory is properly deallocated. Here's an example:

```cpp
{
    std::unique_ptr<int> ptr(new int(42));
    // ... do something with ptr
} // ptr's destructor called, memory deallocated
```

In this example, the memory allocated for the `int` object is released when the `std::unique_ptr` goes out of scope.

## `std::shared_ptr`

`std::shared_ptr` is a reference-counted smart pointer that allows multiple pointers to share ownership of the same underlying resource. It keeps track of the number of references to the object and deallocates the memory only when the last `std::shared_ptr` pointing to the resource is destroyed or reset.

The destructor of `std::shared_ptr` decreases the reference count. If the count reaches zero, meaning no more shared pointers are referencing the resource, the destructor performs the deallocation. Here's an example:

```cpp
{
    std::shared_ptr<int> ptr1(new int(42));
    std::shared_ptr<int> ptr2 = ptr1; // Increase reference count

    // ... do something with ptr1 and ptr2

} // ptr1 and ptr2's destructors called, memory deallocated if ref count is zero
```

In this example, the memory allocated for the `int` object is deallocated when both `ptr1` and `ptr2` go out of scope.

## Conclusion

Understanding the destructor behavior of `std::unique_ptr` and `std::shared_ptr` is crucial for proper memory management. `std::unique_ptr` deallocates memory when it goes out of scope, while `std::shared_ptr` deallocates memory only when the last reference to the resource is destroyed.

By utilizing these smart pointers correctly, you can ensure efficient and safe memory handling in your C++ code.

#programming #Cplusplus