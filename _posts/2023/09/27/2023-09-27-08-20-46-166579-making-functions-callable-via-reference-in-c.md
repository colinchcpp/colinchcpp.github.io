---
layout: post
title: "Making functions callable via reference in C++"
description: " "
date: 2023-09-27
tags: [FunctionPointers, CallableReference]
comments: true
share: true
---

Functions in C++ are typically called using the function name followed by parentheses and arguments. However, in some cases, it may be useful to treat a function as an object and pass it around as a reference. This allows for more flexibility and can be handy in scenarios like callback functions or event handling.

## Function Pointers

In C++, one way to make functions callable via reference is by using function pointers. A function pointer holds the address of a function, allowing it to be called indirectly through the pointer. Here's an example:

```cpp
#include <iostream>

void sayHello() {
    std::cout << "Hello, World!" << std::endl;
}

int main() {
    void (*funcPtr)() = sayHello;   // Function pointer declaration and assignment
    funcPtr();                      // Function call via pointer

    return 0;
}
```
In the code above, we declare a function `sayHello()`, which prints "Hello, World!". Then, we declare a function pointer `funcPtr` of type `void (*)()`, where `void` represents the return type, and `(*)()` indicates that it's a pointer to a function taking no arguments. We assign the address of `sayHello` to `funcPtr` and call the function using the pointer.

## std::function

Another more modern way to make functions callable via reference is by using `std::function` from the C++ Standard Library. `std::function` provides a flexible and type-safe way to store and invoke callable objects, including functions, function pointers, and lambda expressions.

```cpp
#include <iostream>
#include <functional>

void sayHello() {
    std::cout << "Hello, World!" << std::endl;
}

int main() {
    std::function<void()> func = sayHello;  // std::function declaration and assignment
    func();                                 // Function call via std::function

    return 0;
}
```

In the code snippet above, we include the `<functional>` header and use `std::function` to create a variable `func` of type `std::function<void()>`, which represents a callable taking no arguments and returning `void`. We assign the function `sayHello` to `func` and call it using the `operator()` of `std::function`.

## Conclusion

By using function pointers or `std::function`, we can make functions callable via reference in C++. These techniques provide greater flexibility and enable scenarios such as callback functions and event handling. Function pointers allow for direct assignment and calling, while `std::function` provides a more generic and type-safe approach. Choose the method that best fits your needs and make your functions callable via reference in C++.

#C++ #FunctionPointers #CallableReference