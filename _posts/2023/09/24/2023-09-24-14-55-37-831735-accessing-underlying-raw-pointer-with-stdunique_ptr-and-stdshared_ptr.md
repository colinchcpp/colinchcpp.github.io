---
layout: post
title: "Accessing underlying raw pointer with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [SmartPointers]
comments: true
share: true
---

## Accessing the Raw Pointer in `std::unique_ptr`

`std::unique_ptr` is designed to provide exclusive ownership of the managed resource. It is not recommended to directly access the raw pointer held by `std::unique_ptr` as it can lead to double deletion or undefined behavior. However, there are cases where you might still need to access the raw pointer, such as when interfacing with legacy code or external libraries.

To access the raw pointer from `std::unique_ptr`, you can use the `get()` member function. Here's an example:

```cpp
std::unique_ptr<int> myPtr = std::make_unique<int>(42);
int* rawPtr = myPtr.get();
```

In the above code, the `get()` function returns the raw pointer held by `myPtr`. It is important to note that `std::unique_ptr` still owns the resource, and you should not delete the raw pointer yourself.

## Accessing the Raw Pointer in `std::shared_ptr`

Unlike `std::unique_ptr`, `std::shared_ptr` allows multiple instances to share ownership of the managed resource. It keeps track of the reference count and automatically deletes the resource when no `std::shared_ptr` is pointing to it.

To access the raw pointer in `std::shared_ptr`, you can use the `get()` member function, similar to `std::unique_ptr`. Here's an example:

```cpp
std::shared_ptr<int> myPtr = std::make_shared<int>(42);
int* rawPtr = myPtr.get();
```

The `get()` function returns the raw pointer, allowing you to access the underlying data. However, be cautious when using the raw pointer, as it does not manage the reference count like `std::shared_ptr` does.

## Summary

While it is generally recommended to avoid accessing the raw pointer held by `std::unique_ptr` and `std::shared_ptr`, there might be cases where it is necessary. By using the `get()` member function, you can safely access the raw pointer for specific requirements. However, remember to exercise caution and avoid manually deleting or modifying the raw pointer, as it may lead to memory leaks or undefined behavior.

#C++ #SmartPointers