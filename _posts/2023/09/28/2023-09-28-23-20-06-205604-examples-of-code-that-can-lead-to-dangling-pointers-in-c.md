---
layout: post
title: "Examples of code that can lead to dangling pointers in C++"
description: " "
date: 2023-09-28
tags: [DanglingPointers]
comments: true
share: true
---

Dangling pointers are a common issue in C++ that can lead to unexpected behavior and even crashes in your code. A dangling pointer is a pointer that points to memory that has been deallocated or is no longer valid. Here are a few examples of code that can lead to dangling pointers.

## 1. Returning a pointer to a local variable

```cpp
int* createLocalPointer() {
    int num = 42;
    int* ptr = &num;
    return ptr;   // Returning a pointer to a local variable
}

int main() {
    int* danglingPtr = createLocalPointer();
    // After the function exits, danglingPtr points to memory that is no longer valid
    // Accessing it would lead to undefined behavior.
    return 0;
}
```
Hashtags: #DanglingPointers #C++ 

In this example, we are creating a local integer variable `num` and then returning a pointer to it. However, once the function `createLocalPointer()` returns, the local variable `num` goes out of scope, and the memory it occupied is deallocated. The pointer `danglingPtr` now points to invalid memory.

## 2. Using a pointer after deallocation

```cpp
int* createDynamicPointer() {
    int* ptr = new int(42);
    return ptr;
}

int main() {
    int* validPtr = createDynamicPointer();
    delete validPtr;   // Deallocating the memory pointed by validPtr
    
    // Accessing validPtr after deallocation leads to a dangling pointer.
    // Undefined behavior can occur if you try to use it.
    return 0;
}
```

In this example, we are dynamically allocating memory using the `new` operator and assigning its address to a pointer `validPtr`. Then, we deallocate the memory using the `delete` statement. However, if we try to access `validPtr` after the deallocation, it will become a dangling pointer.

It's essential to handle pointers carefully in C++. Avoid creating dangling pointers by making sure that the pointers always point to valid memory locations.