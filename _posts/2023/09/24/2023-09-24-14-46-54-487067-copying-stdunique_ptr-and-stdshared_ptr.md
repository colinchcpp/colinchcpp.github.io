---
layout: post
title: "Copying `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [smartpointers, stdunique_ptr]
comments: true
share: true
---

Copying smart pointers like `std::unique_ptr` and `std::shared_ptr` can be tricky due to their ownership semantics and non-copyable nature. In this blog post, we will explore how to correctly handle copying and assignment with these smart pointers.

## Copying `std::unique_ptr`
`std::unique_ptr` is designed to have exclusive ownership of an object. As the name suggests, it is unique, meaning it cannot be copied directly. When we want to transfer ownership of the managed object to another `std::unique_ptr`, we should use `std::move`.

```cpp
std::unique_ptr<int> source = std::make_unique<int>(42);
std::unique_ptr<int> destination = std::move(source);
```
In the above code, we transfer ownership of the `source` pointer to the `destination` pointer using `std::move`. After the transfer, `source` is set to `nullptr`, indicating the ownership has been moved.

Attempting to create a copy of a `std::unique_ptr` will result in a compilation error.

## Copying `std::shared_ptr`
`std::shared_ptr` allows multiple owners to share ownership of the same object. Unlike `std::unique_ptr`, `std::shared_ptr` is copyable. Each copy of the `std::shared_ptr` shares ownership and keeps a reference count. The object is only deleted when the last `std::shared_ptr` holding it is destroyed.

```cpp
std::shared_ptr<int> source = std::make_shared<int>(42);
std::shared_ptr<int> copy = source;
```

In the above code, both `source` and `copy` share ownership of the same `int` object. The reference count is increased to 2.

It's important to note that copying a `std::shared_ptr` creates a new shared ownership relationship, which might have performance implications due to atomic operations required to increment/decrement the reference count. Therefore, if you only need a local copy that doesn't require owning the object, consider using a `const` reference.

To explicitly release ownership from a `std::shared_ptr`, you can use the `reset()` function.

## Conclusion
Copying smart pointers requires attention to their ownership semantics. While `std::unique_ptr` is not directly copyable, it can be moved using `std::move()`. On the other hand, `std::shared_ptr` allows for shared ownership and easy copying. Consider the ownership requirements and choose the appropriate smart pointer accordingly.

#cpp #smartpointers #stdunique_ptr #stdshared_ptr