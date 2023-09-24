---
layout: post
title: "Memory management with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [smartpointers]
comments: true
share: true
---

## `std::unique_ptr`

The `std::unique_ptr` is a smart pointer that provides unique ownership of dynamically allocated objects. This means that there can be only one `std::unique_ptr` pointing to a particular object. Once the `std::unique_ptr` goes out of scope or is explicitly reset, it automatically releases the associated memory.

Here's how you can use `std::unique_ptr`:

```cpp
std::unique_ptr<int> myUniquePtr(new int(42));
```

In the above code, `myUniquePtr` is a `std::unique_ptr` that points to a dynamically allocated integer with the value `42`.

You can also transfer ownership of a `std::unique_ptr` using the `std::move` function:

```cpp
std::unique_ptr<int> anotherUniquePtr = std::move(myUniquePtr);
```

In the above example, `myUniquePtr` loses ownership of the dynamically allocated integer, and `anotherUniquePtr` becomes the new owner.

## `std::shared_ptr`

While `std::unique_ptr` is great for handling exclusive ownership, there are scenarios where shared ownership is required. This is where `std::shared_ptr` comes into play. Unlike `std::unique_ptr`, `std::shared_ptr` allows multiple pointers to point to the same object.

Here's an example of using `std::shared_ptr`:

```cpp
std::shared_ptr<int> mySharedPtr(new int(42));
std::shared_ptr<int> anotherSharedPtr = mySharedPtr;
```

In the above code, both `mySharedPtr` and `anotherSharedPtr` point to the same dynamically allocated integer with the value `42`. The reference count of the underlying object is maintained internally by the `std::shared_ptr`.

Once all the `std::shared_ptr` instances that point to the object go out of scope, the memory is automatically deallocated.

It's important to note that `std::shared_ptr` uses atomic operations to ensure thread-safe reference counting, making it safe to use in multithreaded environments.

## Conclusion

Both `std::unique_ptr` and `std::shared_ptr` are powerful tools for memory management in C++. By using smart pointers, we can avoid many of the pitfalls associated with manual memory management, such as memory leaks and double deletion. When deciding between `std::unique_ptr` and `std::shared_ptr`, consider the ownership requirements of your code and choose the appropriate smart pointer accordingly.

#C++ #smartpointers