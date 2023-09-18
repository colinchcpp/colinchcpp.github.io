---
layout: post
title: "How to create functors with variable arguments in C++"
description: " "
date: 2023-09-14
tags: [Functors]
comments: true
share: true
---

In C++, a functor is a class or struct that behaves like a function. By overloading the `operator()` function, you can use an instance of a functor like a function.

Creating a functor with variable arguments in C++ allows you to pass a varying number of arguments to the functor. This can be useful in scenarios where you need flexibility in terms of the number of arguments passed.

Here's an example of how to create functors with variable arguments in C++:

```cpp
#include <iostream>
#include <functional>

// Functor class with variable arguments
class MyFunctor {
public:
    // Overload operator()
    template<typename... Args>
    void operator()(Args... args) const {
        std::cout << "Number of arguments: " << sizeof...(args) << std::endl;
        PrintArguments(args...);
    }

private:
    // Helper function to print arguments
    template<typename T>
    void PrintArguments(T arg) const {
        std::cout << arg << std::endl;
    }

    template<typename T, typename... Args>
    void PrintArguments(T arg, Args... args) const {
        std::cout << arg << std::endl;
        PrintArguments(args...);
    }
};

int main() {
    // Create instance of MyFunctor
    MyFunctor myFunctor;

    // Call the functor with different number of arguments
    myFunctor(1, 2, 3);               // Outputs: Number of arguments: 3, 1, 2, 3
    myFunctor("Hello", 'A', 4.5);     // Outputs: Number of arguments: 3, Hello, A, 4.5

    return 0;
}
```

In the example code above, the `MyFunctor` class is defined with a templated `operator()` overloaded function. The `sizeof...(args)` expression is used to determine the number of arguments passed to the functor.

The `PrintArguments` helper function is recursively called to print all the arguments passed to the functor. This is achieved through variadic templates, where each argument is printed and then the function calls itself with the remaining arguments.

By running the `main()` function, you will see that the functor can accept a varying number of arguments and print them accordingly.

Using functors with variable arguments can bring flexibility and extensibility to your C++ code. It allows you to create generic function objects that can handle different scenarios without the need for function overloading.

#C++ #Functors