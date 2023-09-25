---
layout: post
title: "Constructors for Function Pointers in C++"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In C++, function pointers provide a powerful mechanism to store and call functions dynamically. They can be used to achieve flexibility and extensibility in your code. In this blog post, we will explore how to define constructors for function pointers in C++.

## What are Function Pointers?
A function pointer is a variable that can be used to store the address of a function. It allows us to treat functions as first-class objects, enabling us to pass functions as arguments, return functions from other functions, and store functions in data structures.

## Defining a Function Pointer
Before we dive into constructors for function pointers, let's quickly review the syntax for declaring a function pointer:

```cpp
return_type (*pointer_name)(arguments);
```

Here, `return_type` is the return type of the function, `pointer_name` is the name of the pointer variable, and `arguments` are the arguments of the function.

## Constructor for Function Pointers
In C++, we can define constructors for function pointers using function types as parameters. The constructor initializes the function pointer to point to a specific function.

```cpp
#include <iostream>

// Function type
using FunctionType = void (*)(int);

class FunctionPointer {
public:
    // Constructor
    FunctionPointer(FunctionType func) : m_func(func) {}

    // Execute the stored function
    void execute(int value) {
        m_func(value);
    }

private:
    FunctionType m_func;
};

// Sample functions
void printNumber(int number) {
    std::cout << "Number: " << number << std::endl;
}

void printSquare(int number) {
    std::cout << "Square: " << (number * number) << std::endl;
}

int main() {
    // Create function pointer objects
    FunctionPointer ptr1(printNumber);
    FunctionPointer ptr2(printSquare);

    // Call the execute method to invoke the stored functions
    ptr1.execute(5);  // Output: Number: 5
    ptr2.execute(5);  // Output: Square: 25

    return 0;
}
```

In the above example, we define a class called `FunctionPointer` to encapsulate the function pointer. The constructor takes a function of type `FunctionType` as a parameter and initializes the member variable `m_func` with the passed function.

We then create objects of the `FunctionPointer` class, passing the desired functions to the constructor. The `execute` method is used to invoke the stored functions with a given value.

## Conclusion
Constructors for function pointers allow us to conveniently initialize function pointers and store them in objects. This enables us to achieve greater flexibility in our code and implement dynamic function calling in C++.