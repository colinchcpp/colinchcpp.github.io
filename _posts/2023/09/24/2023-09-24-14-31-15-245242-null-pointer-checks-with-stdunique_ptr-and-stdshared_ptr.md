---
layout: post
title: "Null pointer checks with `std::unique_ptr` and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

Both `std::unique_ptr` and `std::shared_ptr` are part of the `<memory>` header and can be used as safer alternatives to raw pointers. They provide automatic memory deallocation and null pointer checks, thereby reducing the chances of null pointer exceptions.

## `std::unique_ptr`

`std::unique_ptr` is a smart pointer that manages the lifetime of an object allocated on the heap. It guarantees exclusive ownership of the object and ensures that at any given time, only one `std::unique_ptr` can own the object.

To perform null pointer checks with `std::unique_ptr`, you can utilize its member function `get()`, which returns a pointer to the managed object or `nullptr` if the pointer is empty. Here's an example:

```cpp
#include <memory>

int main() {
    std::unique_ptr<int> ptr = nullptr;
    if (ptr.get() == nullptr) {
        // Null pointer check
        // Handle the null case
    } else {
        // Pointer is not null
        // Proceed with the logic
    }

    return 0;
}
```

In the above example, we use the `get()` function to check whether the `std::unique_ptr` is pointing to a valid object or is `nullptr`.

## `std::shared_ptr`

`std::shared_ptr` is another smart pointer that allows multiple pointers to share ownership of the same object. It keeps track of the number of shared references to the object and deallocates the memory when all the references are gone.

Similar to `std::unique_ptr`, you can perform null pointer checks with `std::shared_ptr` using its `get()` member function. Here's an example:

```cpp
#include <memory>

int main() {
    std::shared_ptr<int> ptr = nullptr;
    if (ptr.get() == nullptr) {
        // Null pointer check
        // Handle the null case
    } else {
        // Pointer is not null
        // Proceed with the logic
    }
    
    return 0;
}
```

The `get()` function ensures that you can check whether the `std::shared_ptr` is pointing to a valid memory location or if it is `nullptr`.

By leveraging `std::unique_ptr` and `std::shared_ptr` along with null pointer checks, you can significantly reduce the chances of encountering null pointer exceptions in your C++ code. This not only makes your code more robust but also improves its overall stability and reliability.

#coding #C++