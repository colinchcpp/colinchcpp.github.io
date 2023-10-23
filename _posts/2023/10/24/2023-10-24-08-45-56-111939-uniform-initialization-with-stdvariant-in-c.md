---
layout: post
title: "Uniform initialization with std::variant in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, `std::variant` is a type-safe union that can hold values of different types. It provides a way to store and manipulate objects of different types in a single variable. 

Before C++17, initializing a `std::variant` required some boilerplate code. However, with C++17's uniform initialization syntax, initializing a `std::variant` becomes much simpler and more intuitive.

## Initializing a `std::variant`

To initialize a `std::variant`, you can use the uniform initialization syntax with the types enclosed in curly braces `{}`. The compiler will automatically determine the appropriate type based on the provided values. Here's an example:

```cpp
#include <variant>
#include <iostream>

struct Integer {
    int value;
};

struct Float {
    float value;
};

int main() {
    std::variant<int, float> var{42};    // Initializing with an int
    std::visit([](auto value) {
        // Handling the variant based on the type
        if constexpr (std::is_same_v<decltype(value), int>) {
            std::cout << "It's an int: " << value << std::endl;
        } else if constexpr (std::is_same_v<decltype(value), float>) {
            std::cout << "It's a float: " << value << std::endl;
        }
    }, var);

    var = {3.14f};    // Initializing with a float
    std::visit([](auto value) {
        // Handling the updated variant based on the type
        if constexpr (std::is_same_v<decltype(value), int>) {
            std::cout << "It's still an int: " << value << std::endl;
        } else if constexpr (std::is_same_v<decltype(value), float>) {
            std::cout << "It's now a float: " << value << std::endl;
        }
    }, var);
    
    return 0;
}
```

In the example above, we have a `std::variant` that can hold either an `int` or a `float`. By using the uniform initialization syntax with the provided values, the compiler deduces the appropriate type for the `std::variant`. We can then use `std::visit` to handle the variant based on its current type.

## Conclusion

Uniform initialization with `std::variant` in C++17 simplifies the process of initializing and working with a `std::variant`. It allows you to initialize a `std::variant` using a more concise and intuitive syntax, reducing boilerplate code and making your code more readable. This feature is especially useful when dealing with scenarios where the type of the `std::variant` can change dynamically during runtime.