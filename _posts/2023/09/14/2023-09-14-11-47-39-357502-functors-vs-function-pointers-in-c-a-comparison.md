---
layout: post
title: "Functors vs. function pointers in C++: a comparison"
description: " "
date: 2023-09-14
tags: [include, include, FunctionPointers, Functors]
comments: true
share: true
---

When it comes to C++, there are multiple ways to pass functions as arguments to other functions or store them in data structures. Two common approaches are using functors and function pointers. In this post, we will compare these two techniques and discuss their advantages and use cases.

## Function Pointers

Function pointers in C++ provide a way to store the address of a function and invoke it later. Here's an example that demonstrates the usage of function pointers:

```cpp
#include <iostream>

void greet() {
    std::cout << "Hello, World!" << std::endl;
}

int add(int a, int b) {
    return a + b;
}

int main() {
    void (*funcPtr)() = greet;
    funcPtr(); // Call the function through the function pointer

    int (*addPtr)(int, int) = add;
    int result = addPtr(3, 4);
    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

In the above code, we define two functions - `greet` and `add`. We then declare function pointers `funcPtr` and `addPtr`, which store the addresses of the respective functions. We can later invoke these functions through their function pointers.

Function pointers have the advantage of being lightweight and directly callable. They are especially useful in cases where you need to dynamically switch between different functions at runtime.

## Functors

Functors, or function objects, are objects that behave like functions. They can be instances of a class that overloads the function call operator `()`. Here's an example illustrating the usage of functors:

```cpp
#include <iostream>

class Greet {
public:
    void operator()() {
        std::cout << "Hello, World!" << std::endl;
    }
};

class Add {
public:
    int operator()(int a, int b) {
        return a + b;
    }
};

int main() {
    Greet greet;
    greet();

    Add add;
    int result = add(3, 4);
    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

In this code snippet, we define two classes - `Greet` and `Add`. These classes override the function call operator `()` to make instances of the classes callable like functions. We then create instances of `Greet` and `Add` and invoke them as if they were functions.

Functors are more powerful than function pointers because they can hold state and have additional member functions. They are often used in scenarios where we need to encapsulate a group of related functions along with some extra functionality.

## Conclusion

Both functors and function pointers provide ways to pass functions around in C++. Function pointers are lightweight and directly callable, ideal for dynamically switching between functions at runtime. On the other hand, functors offer more flexibility and can hold state and additional member functions. They are suitable when we need to encapsulate functions along with extra functionality.

Understanding the differences between functors and function pointers helps to choose the most appropriate approach for a given situation. By leveraging these techniques effectively, C++ developers can write more flexible and powerful code.

#C++ #FunctionPointers #Functors