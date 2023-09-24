---
layout: post
title: "Copying `std::unique_ptr` and `std::shared_ptr` objects"
description: " "
date: 2023-09-24
tags: [SmartPointers]
comments: true
share: true
---

When working with smart pointers in C++, such as `std::unique_ptr` and `std::shared_ptr`, it's important to understand their ownership semantics and how they handle copying and moving.

## Understanding `std::unique_ptr`
`std::unique_ptr` is designed to have exclusive ownership of an object and does not support direct copying. Only one `std::unique_ptr` can own the underlying resource at a given time. However, you can transfer ownership using move semantics.

```cpp
std::unique_ptr<int> ptr1 = std::make_unique<int>(42);
std::unique_ptr<int> ptr2 = std::move(ptr1); // Transfer ownership

// Access the underlying object
std::cout << *ptr2 << std::endl; // Output: 42
```

In the example above, we first create a `std::unique_ptr` `ptr1` that owns an `int` with the value 42. Then, we transfer ownership of the object from `ptr1` to `ptr2` using the `std::move` function. Finally, we can still access the underlying object through `ptr2`.

## Working with `std::shared_ptr`
`std::shared_ptr` allows multiple pointers to share ownership of the same object. It keeps track of the number of references to the underlying object and automatically deletes the object when the last `std::shared_ptr` goes out of scope.

```cpp
std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
std::shared_ptr<int> ptr2 = ptr1; // Shared ownership

// Access the underlying object
std::cout << *ptr1 << std::endl; // Output: 42
std::cout << *ptr2 << std::endl; // Output: 42
```

In the above example, `ptr1` and `ptr2` both share ownership of the same `int` object. When one of them goes out of scope, the reference count will decrease, but the object itself won't be deleted until the last `std::shared_ptr` referencing it is destroyed.

## Copying `std::shared_ptr` Objects
If you want to create a copy of a `std::shared_ptr`, you can simply assign it to another `std::shared_ptr` or use the copy constructor. This increases the reference count of the underlying object.

```cpp
std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
std::shared_ptr<int> ptr2 = ptr1; // Copying
std::shared_ptr<int> ptr3(ptr2); // Using the copy constructor

// Access the underlying object
std::cout << *ptr1 << std::endl; // Output: 42
std::cout << *ptr2 << std::endl; // Output: 42
std::cout << *ptr3 << std::endl; // Output: 42
```

In the example above, both `ptr2` and `ptr3` now share ownership of the same `int` object as `ptr1`. The reference count is updated accordingly.

## Important Considerations
- Keep in mind that copying a `std::unique_ptr` will cause a compilation error because it violates the exclusive ownership principle.
- When using `std::shared_ptr`, copying is generally safe, but be mindful of creating circular references, as they can lead to memory leaks.
- Always ensure that you properly manage the ownership semantics when working with smart pointers to avoid dangling references or memory leaks.

**#C++ #SmartPointers**