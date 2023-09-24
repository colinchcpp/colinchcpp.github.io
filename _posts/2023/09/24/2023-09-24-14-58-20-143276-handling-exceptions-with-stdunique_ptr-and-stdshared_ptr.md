---
layout: post
title: "Handling exceptions with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [ExceptionHandling, SmartPointers]
comments: true
share: true
---

## Exception Safety Guarantees
Before diving into handling exceptions with smart pointers, it's essential to understand exception safety guarantees provided by C++. There are three levels of exception safety:

1. **No-throw guarantee**: The operation will never throw an exception.
2. **Strong exception safety guarantee**: If an exception occurs, the object's state will remain unchanged.
3. **Basic exception safety guarantee**: If an exception occurs, the object's state may be modified but remains in a valid and usable state.

## Using `std::unique_ptr`
`std::unique_ptr` provides a lightweight mechanism for exclusive ownership of a dynamically allocated object. When an exception is thrown during object construction, the memory allocated by `std::unique_ptr` is automatically deallocated, ensuring proper resource cleanup. However, if an exception is thrown in the constructor of the pointed object, the `std::unique_ptr` itself will not be destroyed. To handle such exceptions, you can use the following approach:

```cpp
std::unique_ptr<MyClass> createMyClass() {
    std::unique_ptr<MyClass> ptr;
    try {
        ptr = std::make_unique<MyClass>(); // Potential exception
        ptr->initialize(); // Potential exception
    } catch (...) {
        // Handle exception
        throw; // Re-throw the exception
    }
    return ptr;
}
```  

In the above code snippet, we create a `std::unique_ptr` called `ptr` and initialize it within a try block. If an exception occurs during the object creation or initialization, the catch block is executed. Here, you can handle the exception as needed and re-throw it to maintain exception safety.

## Using `std::shared_ptr`
`std::shared_ptr` allows multiple pointers to share ownership of the same object. When an exception is thrown during object construction or destruction, the `std::shared_ptr` automatically deallocates the memory, ensuring proper cleanup.
 
```cpp
std::shared_ptr<MyClass> createMyClass() {
    std::shared_ptr<MyClass> ptr;
    try {
        ptr = std::make_shared<MyClass>(); // Potential exception
        ptr->initialize(); // Potential exception
    } catch (...) {
        // Handle exception
        throw; // Re-throw the exception
    }
    return ptr;
}
```

Similarly to `std::unique_ptr`, when using `std::shared_ptr`, we should enclose the construction and initialization of the object within a try block and handle any potential exceptions that may occur.

## Conclusion
When using smart pointers like `std::unique_ptr` and `std::shared_ptr`, it's important to handle exceptions properly to ensure resource cleanup. By enclosing object construction and initialization within a try block and handling any potential exceptions, we can achieve robust and exception-safe code. Remember, exception safety guarantees are vital for writing reliable and maintainable software.

#C++ #ExceptionHandling #SmartPointers