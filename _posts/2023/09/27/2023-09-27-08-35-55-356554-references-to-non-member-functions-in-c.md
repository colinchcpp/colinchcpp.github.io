---
layout: post
title: "References to non-member functions in C++"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

Here are a few examples of how to reference non-member functions in C++:

1. Function Pointers:
One way to reference a non-member function is by using function pointers. Function pointers are C++ language features that allow you to store the address of a function and call it later.

```cpp
#include <iostream>

void printMessage(const std::string& message) {
    std::cout << message << std::endl;
}

int main() {
    void (*funcPtr)(const std::string&) = &printMessage;   // Function pointer declaration and assignment

    // Calling the non-member function using the function pointer
    (*funcPtr)("Hello, World!");

    return 0;
}
```

In the example above, the `printMessage` function is defined as a non-member function. We declare a function pointer `funcPtr` that points to this non-member function. We then call the non-member function using this function pointer.

2. Lambda Functions:
Another way to reference a non-member function is by using lambda functions. Lambda functions are anonymous functions that can be defined inline.

```cpp
#include <iostream>

void forEach(const std::string& message, const std::function<void(const std::string&)>& action) {
    // Call the action function on each character of the message
    for (char c : message) {
        action(std::string(1, c));
    }
}

int main() {
    std::string message = "Hello, World!";

    // Define a lambda function as a non-member function
    auto printChar = [](const std::string& c) {
        std::cout << c << std::endl;
    };

    // Call the non-member function using lambda function
    forEach(message, printChar);

    return 0;
}
```

In the above example, the `forEach` function is a non-member function that takes a string `message` and a function `action` as parameters. We define a lambda function `printChar` inline and pass it as the `action` parameter to `forEach`. The non-member function is then called using the lambda function.

Referencing non-member functions in C++ allows for greater flexibility and modularity in your code. Function pointers and lambda functions are powerful features that enable you to pass and use non-member functions in various scenarios.