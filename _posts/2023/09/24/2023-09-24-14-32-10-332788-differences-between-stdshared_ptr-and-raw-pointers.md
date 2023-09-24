---
layout: post
title: "Differences between `std::shared_ptr` and raw pointers"
description: " "
date: 2023-09-24
tags: [MemoryManagement]
comments: true
share: true
---

In C++, there are multiple ways to manage memory and handle object ownership. Two commonly used approaches are `std::shared_ptr` and raw pointers. While both can point to objects and access their members, there are some crucial differences between them.

### Ownership
- **Raw Pointers**: With raw pointers, there is no automatic management of memory ownership. Developers must remember to manually allocate and deallocate memory. It is easy to encounter memory leaks or dangling pointers if proper care is not taken.

- **std::shared_ptr**: In contrast, `std::shared_ptr` uses the concept of **shared ownership**. Multiple `std::shared_ptr` objects can hold a reference to the same object. The underlying memory is automatically managed and deallocated when the last `std::shared_ptr` pointing to it is destroyed or reset.

### Lifetime
- **Raw Pointers**: Raw pointers have a more flexible lifetime. They can be created, copied, and destroyed at any point in the code. The developer is responsible for manually managing the lifetime of the object they point to.

- **std::shared_ptr**: `std::shared_ptr` has a **fixed lifetime** determined by its reference count. When the reference count reaches zero, i.e., no more `std::shared_ptr` objects point to the managed object, the memory is deallocated. This ensures that the object stays alive as long as there are active `std::shared_ptr` instances referencing it.

### Copying and Ownership Transfer
- **Raw Pointers**: Raw pointers can be easily copied by assigning their value to another raw pointer. This operation transfers ownership of the pointed object, and both pointers will have access to it. Manual memory management is crucial to avoid memory leaks or double deletions.

- **std::shared_ptr**: `std::shared_ptr` uses reference counting to manage ownership. Copying a `std::shared_ptr` using assignment or by passing it to a function **increases the reference count**. The object will only be deallocated when the reference count reaches zero.

### Nullability
- **Raw Pointers**: Raw pointers can be `nullptr` to represent a null pointer, indicating that they do not point to any valid object.

- **std::shared_ptr**: `std::shared_ptr` can also be `nullptr` to indicate that they do not point to any valid object.

### Thread Safety
- **Raw Pointers**: Raw pointers do not provide inherent thread safety. Developers must implement their own synchronization mechanisms when sharing raw pointers across multiple threads.

- **std::shared_ptr**: `std::shared_ptr` uses atomic operations for reference count updates, making it safer to use in multi-threaded environments.

### Hashtags: #Cpp #MemoryManagement