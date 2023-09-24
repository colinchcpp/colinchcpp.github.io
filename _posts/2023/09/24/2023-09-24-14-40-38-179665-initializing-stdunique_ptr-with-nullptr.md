---
layout: post
title: "Initializing `std::unique_ptr` with nullptr"
description: " "
date: 2023-09-24
tags: [include]
comments: true
share: true
---

When working with `std::unique_ptr`, you might come across scenarios where you need to initialize a pointer with a null value. This can be done by using `nullptr`, which is a keyword introduced in C++11 to represent a null pointer value.

To initialize a `std::unique_ptr` with `nullptr`, you can simply assign `nullptr` to the pointer using the assignment operator or use the `make_unique` function with `nullptr` as the argument.

Here's an example of initializing a `std::unique_ptr` with `nullptr`:

```cpp
#include <memory>

int main() {
    // Using the assignment operator
    std::unique_ptr<int> ptr = nullptr;

    // Using make_unique with nullptr
    std::unique_ptr<int> ptr2 = std::make_unique<int>(nullptr);
    
    return 0;
}
```

In the above code, we are creating two `std::unique_ptr` objects `ptr` and `ptr2` and initializing them with `nullptr`. It's important to note that assigning `nullptr` to `std::unique_ptr` sets the pointer to be empty, meaning it doesn't point to an object.

Initializing `std::unique_ptr` with `nullptr` can be handy when you want to indicate that the pointer doesn't currently own any object. It's also useful as an initial value before setting the pointer to point to a valid object.

By using `std::unique_ptr` in conjunction with `nullptr`, you can ensure safer and more predictable memory management in your C++ code.