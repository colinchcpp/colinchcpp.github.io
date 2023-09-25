---
layout: post
title: "Using `std::shared_ptr` with raw pointers"
description: " "
date: 2023-09-24
tags: [SmartPointers]
comments: true
share: true
---

To use `std::shared_ptr` with raw pointers, you first need to understand what a smart pointer is. A smart pointer is an object that acts like a pointer to dynamically allocated memory but also provides automatic memory management. `std::shared_ptr` is a type of smart pointer that uses reference counting to keep track of how many objects are referencing the same dynamically allocated memory.

Here's an example of using `std::shared_ptr` with a raw pointer:

```cpp
#include <memory>

int main() {
    int* rawPtr = new int(5);  // Create a raw pointer to dynamically allocated memory

    std::shared_ptr<int> sharedPtr(rawPtr);  // Create a shared_ptr from the raw pointer

    // Access the value through the shared_ptr
    std::cout << *sharedPtr << std::endl;  // Output: 5

    // Use the shared_ptr just like a raw pointer
    *sharedPtr = 10;

    // No need to manually deallocate memory
    // The memory will be automatically deallocated when there are no more references

    return 0;
}
```

In the example above, we first create a raw pointer `rawPtr` and allocate memory to store an integer value of 5. Then, we create a `std::shared_ptr<int>` named `sharedPtr` and pass the `rawPtr` to its constructor. 

Since `std::shared_ptr` uses reference counting, it keeps track of the number of objects referring to the same memory. When the reference count reaches zero, meaning there are no more references to the memory, the `std::shared_ptr` destructor deallocates the memory automatically. This eliminates the need for manual memory management, reducing the chances of memory leaks or accessing deallocated memory.

Using `std::shared_ptr` with raw pointers helps to ensure proper memory management without sacrificing the flexibility and power of using pointers in C++. 

#C++ #SmartPointers