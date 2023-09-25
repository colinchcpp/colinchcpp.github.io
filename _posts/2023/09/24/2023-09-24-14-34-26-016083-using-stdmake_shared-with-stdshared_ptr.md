---
layout: post
title: "Using `std::make_shared` with `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In C++, `std::shared_ptr` is a smart pointer that allows multiple pointers to share ownership of the same object. It manages the lifetime of the underlying object, automatically deallocating it when the last `std::shared_ptr` pointing to it is destroyed. To create a `std::shared_ptr`, you can make use of the `std::make_shared` function.

### The `std::make_shared` Function

The `std::make_shared` function is a helper function provided by the C++ Standard Library that creates a `std::shared_ptr` object and initializes it with a new dynamically allocated object of the specified type. It combines memory allocation and object construction in a single step, maximizing performance and memory efficiency.

The syntax for using `std::make_shared` is as follows:

```cpp
std::shared_ptr<T> ptr = std::make_shared<T>(args);
```

Here, `T` is the type of the object you want to create, and `args` are the arguments to be passed to the object's constructor.

### Advantages of Using `std::make_shared`

Using `std::make_shared` instead of the traditional `std::shared_ptr` constructor has several advantages:

1. **Efficiency**: `std::make_shared` performs a single allocation to create both the object and the control block that manages it, reducing memory overhead.
2. **Exception Safety**: `std::make_shared` ensures exception safety by guaranteeing that memory will be deallocated if an exception occurs during object construction.
3. **Easier to Read**: The syntax is concise and self-explanatory, making the code easier to read and understand.

### Example Usage

Let's consider an example where we want to create a shared pointer to an integer using `std::make_shared`:

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> ptr = std::make_shared<int>(42);
    
    std::cout << *ptr << std::endl; // Output: 42
    
    return 0;
}
```

In the above code, we create a `std::shared_ptr<int>` named `ptr` using `std::make_shared<int>(42)`. The `*ptr` dereferences the pointer, allowing us to access the underlying value and print it to the console.

### Conclusion

Using `std::make_shared` with `std::shared_ptr` provides efficiency, exception safety, and code readability benefits. It is the preferred way to create shared pointers in C++, as it combines memory allocation and object initialization in a single step. By leveraging this functionality, you can write cleaner code and improve the performance of your C++ applications.

\#C++ \#SharedPtr