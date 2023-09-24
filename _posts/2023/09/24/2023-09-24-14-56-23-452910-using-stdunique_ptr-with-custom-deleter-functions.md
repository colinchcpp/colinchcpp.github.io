---
layout: post
title: "Using `std::unique_ptr` with custom deleter functions"
description: " "
date: 2023-09-24
tags: [SmartPointers]
comments: true
share: true
---

By default, `std::unique_ptr` uses the `delete` keyword to free the memory it owns. However, in some cases, we may need to use a custom deleter function instead. This allows us to control how the memory is released, especially when dealing with resources other than raw memory.

To use a custom deleter function with `std::unique_ptr`, we need to provide the function as a template argument when declaring the pointer. Here's an example:

```cpp
// Custom deleter function
void customDeleter(int* ptr) {
    // Custom clean up logic goes here
    delete ptr;
    // Additional clean up steps, if necessary
}

int main() {
    // Using std::unique_ptr with custom deleter
    std::unique_ptr<int, void(*)(int*)> ptr(new int(), customDeleter);

    // The resources will be properly deallocated when ptr goes out of scope
    // Custom deleter function gets called instead of default delete
    // Additional clean up steps, if any, will also be executed

    return 0;
}
```

In the example above, we define a custom deleter function called `customDeleter` that takes an `int*` as its parameter. Inside the function, we perform the necessary clean-up steps for the specific resource we are managing. In this case, we simply use the `delete` keyword to free the memory allocated for the integer.

When declaring the `std::unique_ptr`, we provide the custom deleter function as the second template argument. The `void(*)(int*)` specifies a function pointer type that takes an `int*` and returns `void`. This tells the `std::unique_ptr` to use `customDeleter` for resource deallocation instead of the default `delete` operator.

Using `std::unique_ptr` with custom deleter functions gives us the flexibility to handle resource deallocation in a customized manner. It is particularly useful when dealing with non-standard resources or when additional clean-up steps need to be performed alongside memory deallocation.

#C++ #SmartPointers