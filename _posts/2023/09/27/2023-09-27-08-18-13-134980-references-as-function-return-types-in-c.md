---
layout: post
title: "References as function return types in C++"
description: " "
date: 2023-09-27
tags: [cplusplus, references]
comments: true
share: true
---

Returning a reference from a function allows us to directly access and modify the original object that the referenced value belongs to. This can be useful in scenarios where we want to avoid making copies of large data structures or when we want to modify the original object directly.

To return a reference from a function in C++, we need to declare the return type as a reference type. Let's take a simple example to illustrate this concept:

```cpp
#include <iostream>

// Function that returns a reference to an integer
int& returnReference(int& num) {
    // Modifying the original object
    num *= 2;
    return num; // Returning a reference to the modified object
}

int main() {
    int x = 5;

    // Calling the function and assigning the returned reference to a new variable
    int& ref = returnReference(x);

    std::cout << "x: " << x << std::endl;    // Output: x: 10
    std::cout << "ref: " << ref << std::endl; // Output: ref: 10

    ref = 7; // Modifying the referenced object

    std::cout << "x: " << x << std::endl;    // Output: x: 7
    std::cout << "ref: " << ref << std::endl; // Output: ref: 7

    return 0;
}
```

In the example above, we define a function `returnReference` that takes an integer reference as a parameter. Inside the function, we modify the value of the referenced object and then return the reference itself. We can then assign this returned reference to a variable in the `main` function, allowing us to access and modify the original object directly.

It's important to note that returning references should be done with caution. The lifetime of the referenced object must be longer than the duration of its reference, otherwise accessing the reference can result in undefined behavior.

Using references as function return types can be a powerful tool in C++, enabling us to efficiently work with and modify objects without the need for unnecessary copies. However, it is important to understand the implications and limitations of returning references to ensure correct and safe usage of this feature. #cplusplus #references