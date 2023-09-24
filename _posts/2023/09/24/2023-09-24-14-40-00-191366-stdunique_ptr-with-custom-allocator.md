---
layout: post
title: "`std::unique_ptr` with custom allocator"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

Using a custom allocator with `std::unique_ptr` allows you to have fine-grained control over how memory is allocated and deallocated for the owned object. This can be particularly useful in situations where you need to allocate memory from a specific memory pool or use a different allocation strategy.

To use a custom allocator with `std::unique_ptr`, you need to define a custom deleter that handles the deallocation of the object. Here's an example that demonstrates how to use a custom allocator with `std::unique_ptr`:

```cpp
#include <memory>
#include <iostream>

struct MyDeleter {
    void operator()(int* ptr) {
        std::cout << "Custom deleter is called!" << std::endl;
        // Perform custom deallocation here
        delete ptr;
    }
};

int main() {
    // Create a unique_ptr with a custom allocator
    std::unique_ptr<int, MyDeleter> ptr(new int(42));

    // Use the managed object
    std::cout << *ptr << std::endl;

    // The object will be automatically deallocated
    // when ptr goes out of scope.
    return 0;
}
```

In this example, we define a `MyDeleter` struct which overloads the `operator()` to handle the deallocation of our custom object `int*`. Inside the `operator()`, you can implement your own custom deallocation logic.

When creating the `std::unique_ptr`, we specify the custom deleter type as the second template parameter. In this case, we use `std::unique_ptr<int, MyDeleter>` to define a `std::unique_ptr` that manages an `int` object with our custom deleter.

By using a custom allocator with `std::unique_ptr`, you have control over how memory is allocated and deallocated for the owned object. This allows you to customize the memory management strategy to suit your specific needs.

#C++ #SmartPointers