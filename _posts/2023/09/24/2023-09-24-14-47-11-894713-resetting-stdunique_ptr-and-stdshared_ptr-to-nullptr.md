---
layout: post
title: "Resetting `std::unique_ptr` and `std::shared_ptr` to nullptr"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

The process of resetting a smart pointer to `nullptr` is simple and can be done using the `reset()` member function.

To reset a `std::unique_ptr` to `nullptr`, you can call the `reset()` function without any arguments:

```cpp
std::unique_ptr<int> ptr(new int(42));
ptr.reset(); // Resetting the unique_ptr to nullptr
```

In this example, the `ptr` is initialized with a dynamically allocated integer, after which the `reset()` function is called to set it to `nullptr`.

Similarly, for a `std::shared_ptr`, you can also use the `reset()` function:

```cpp
std::shared_ptr<int> ptr = std::make_shared<int>(42);
ptr.reset(); // Resetting the shared_ptr to nullptr
```

In the above code snippet, the shared pointer `ptr` is created using `std::make_shared<int>(42)`, and then `reset()` is called to reset it to `nullptr`.

By resetting the smart pointer to `nullptr`, you effectively release the ownership of the underlying object, causing the smart pointer to point to nothing. This is particularly useful in scenarios where you want to ensure that a smart pointer doesn't hold onto the object anymore, or when you want to signify the end of the object's lifecycle.

Remember to handle the case where other parts of your code might be expecting the pointer to be valid. Always make sure to null-check the pointer before using it to avoid any potential nullptr dereference errors.

Remember to use smart pointers responsibly and choose the appropriate type (`std::unique_ptr` for exclusive ownership or `std::shared_ptr` for shared ownership) based on your needs.