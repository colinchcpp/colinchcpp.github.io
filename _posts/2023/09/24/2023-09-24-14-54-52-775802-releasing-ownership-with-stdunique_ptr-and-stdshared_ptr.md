---
layout: post
title: "Releasing ownership with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [smartpointers]
comments: true
share: true
---

When working with dynamic memory in C++, it's crucial to ensure proper ownership and management of the allocated resources. The C++11 standard introduced `std::unique_ptr` and `std::shared_ptr`, two smart pointers that simplify memory management by automatically releasing the allocated memory when it's no longer needed.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that allows the ownership of a dynamically allocated object. It ensures that only one `std::unique_ptr` can own the object at a given time, making it impossible to accidentally create multiple pointers to the same object.

```cpp
std::unique_ptr<int> ptr(new int(42));

// Access the value using the dereference operator
int value = *ptr;

// Release ownership and delete the allocated object
ptr.reset();
```

The above code initializes a `std::unique_ptr` with a dynamically allocated integer object. The pointer is then used to access the value using the dereference operator (`*`) and release ownership of the object by calling `reset()`. Upon resetting, the `std::unique_ptr` will automatically delete the allocated object.

## `std::shared_ptr`

`std::shared_ptr` is a smart pointer that allows multiple pointers to share ownership of a dynamically allocated object. It keeps track of the number of `std::shared_ptr` instances pointing to the object and automatically releases the memory when the last pointer goes out of scope.

```cpp
std::shared_ptr<int> ptr1(new int(42));
std::shared_ptr<int> ptr2 = ptr1;

// Access the value using the dereference operator
int value = *ptr1;

// Release ownership of the object managed by ptr1
ptr1.reset();

// Release ownership of the object managed by ptr2
ptr2.reset();
```

In the above example, both `ptr1` and `ptr2` point to the same dynamically allocated integer object. The object will be automatically deleted when both pointers go out of scope or when calling `reset()` explicitly.

## Conclusion

Managing dynamic memory can be a challenging task in C++. With the introduction of `std::unique_ptr` and `std::shared_ptr`, the ownership of dynamically allocated objects can be safely and efficiently handled. `std::unique_ptr` allows exclusive ownership, while `std::shared_ptr` facilitates shared ownership. By using these smart pointers, memory leaks and dangling pointers can be effectively avoided.

#cpp #smartpointers