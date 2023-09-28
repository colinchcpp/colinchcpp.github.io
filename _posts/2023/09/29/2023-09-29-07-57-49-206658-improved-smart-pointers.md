---
layout: post
title: "Improved smart pointers"
description: " "
date: 2023-09-29
tags: [smartpointers, memorymanagement]
comments: true
share: true
---

Smart pointers are an essential part of modern C++ programming. They help manage memory and provide automatic deallocation of resources, ensuring efficient and safe memory management. In this article, we will explore some improvements and additions to smart pointers that further enhance their functionality and usability.

## 1. Shared Pointer with Custom Deleter

The `std::shared_ptr` is a widely used smart pointer that allows multiple owners of a resource. However, in certain scenarios, it is necessary to use a custom deleter to properly release the resource. 

In the latest C++ standards, it is possible to specify a custom deleter for a `std::shared_ptr` using lambda expressions or function objects. This allows you to define the cleanup logic specific to your resource, providing more flexibility and control.

**Example Code:**
```cpp
std::shared_ptr<MyResource> sptr(new MyResource, [](MyResource* resource) {
    // Custom cleanup logic for MyResource
    // ...
    delete resource;
});
```

## 2. Unique Pointer with Array Support

`std::unique_ptr` is another powerful smart pointer that ensures exclusive ownership of a resource. However, it does not directly support managing arrays of dynamically allocated objects.

With the introduction of C++14, the `std::unique_ptr` now supports arrays. This enhancement simplifies memory management, especially when dealing with dynamic arrays. It automatically calls `delete[]` instead of `delete` on the managed pointer, preventing memory leaks.

**Example Code:**
```cpp
std::unique_ptr<int[]> uptr(new int[10]);
for (int i = 0; i < 10; i++) {
    uptr[i] = i;
}
```

## Conclusion

Smart pointers have revolutionized memory management in C++. The improvements discussed in this article provide even more control and flexibility when working with smart pointers.

By using a custom deleter with `std::shared_ptr`, you can define cleanup logic specific to your resource, improving resource management.

The addition of array support to `std::unique_ptr` simplifies memory management when dealing with dynamic arrays, ensuring proper deallocation of memory.

With these improvements, smart pointers continue to evolve and provide developers with safer and more efficient memory management solutions.

#smartpointers #memorymanagement