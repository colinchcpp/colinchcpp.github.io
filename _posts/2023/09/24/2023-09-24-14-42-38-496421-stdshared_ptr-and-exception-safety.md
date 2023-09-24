---
layout: post
title: "`std::shared_ptr` and exception safety"
description: " "
date: 2023-09-24
tags: [include, exception]
comments: true
share: true
---
title: "C++: Exploring std::shared_ptr and Exception Safety"
date: "2021-09-13"
description: "Learn how to use std::shared_ptr and ensure exception safety in your C++ code."
tags: [C++, std::shared_ptr, exception safety]
---

In C++, managing memory is an essential aspect of writing robust and error-free code. The `std::shared_ptr` class from the C++ Standard Library provides a convenient and safe way to manage dynamically allocated objects. In this blog post, we will explore the usage of `std::shared_ptr` and discuss how to ensure exception safety when using it.

## Understanding std::shared_ptr

`std::shared_ptr` is a smart pointer that retains shared ownership of an object through a pointer. Multiple `std::shared_ptr` instances can point to the same object, keeping a reference count internally. The object will be automatically deleted when the last `std::shared_ptr` pointing to it gets destroyed.

You can create a `std::shared_ptr` by using the `std::make_shared` function or directly assigning a pointer to it. Let's see an example:

```cpp
#include <memory>

void foo() {
    // Creating a shared_ptr using make_shared
    std::shared_ptr<int> ptr1 = std::make_shared<int>(42);

    // Creating a shared_ptr from raw pointer
    std::shared_ptr<int> ptr2(new int(21));
}
```

In the above code snippet, we create two `std::shared_ptr` instances `ptr1` and `ptr2` pointing to different `int` objects. It's important to note that you should avoid using `new` directly with `shared_ptr` to avoid potential resource leaks due to exception throws.

## Exception Safety with std::shared_ptr

Achieving exception safety is crucial to ensure your code behaves correctly even when exceptions are thrown. When using `std::shared_ptr`, we need to consider a few guidelines to maintain exception safety:

1. **Use `std::make_shared` for avoiding memory leaks**: The `std::make_shared` function internally manages memory allocation and reference counting. Using it helps to avoid potential memory leaks if an exception occurs during construction.

2. **Avoid using naked `new` with `std::shared_ptr`**: Directly assigning a raw pointer created using `new` to a `std::shared_ptr` can result in resource leaks if exceptions are thrown before the `std::shared_ptr` construction. Always prefer `std::make_shared` or `std::shared_ptr` constructor to initialize pointers.

3. **Wrap potentially throwing operations with exception-safe constructs**: If you have operations that can throw exceptions, it's a good practice to wrap them with exception-safe constructs such as `try-catch` blocks or appropriate exception handling mechanisms. This ensures that resource clean-up is properly handled.

```cpp
void foo() {
    std::shared_ptr<int> ptr;
    try {
        // Perform potentially throwing operation
        ptr = std::make_shared<int>(42);
        // Other code that might throw exceptions
    }
    catch (...) {
        // Handle exceptions
        // Release allocated resources, if necessary
    }
}
```

By following these guidelines, you can ensure that your code using `std::shared_ptr` remains exception-safe and handles exceptions gracefully without causing resource leaks.

## Conclusion

`std::shared_ptr` is a powerful tool in C++ for managing memory and ensuring automatic resource cleanup. By understanding its usage and considering exception safety, you can write more robust and reliable code. Remember to use `std::make_shared` and avoid naked `new` to minimize the chances of resource leaks. Wrap potentially throwing operations with proper exception handling to maintain exception safety in your code.

Keep learning and exploring the various features of C++ to become a more proficient developer!

\#C++ \#std.shared_ptr \#exception-safety