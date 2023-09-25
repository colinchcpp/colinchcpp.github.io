---
layout: post
title: "Constructor Not Called for Temporary Objects in C++"
description: " "
date: 2023-09-23
tags: [Constructors]
comments: true
share: true
---

In C++, constructors are special member functions that are automatically called when an object is instantiated. However, there is a particular scenario where the constructor is not called for temporary objects. Let's explore this situation in more detail.

## Temporary Objects

A temporary object in C++ is an object created during the evaluation of an expression, but it has a limited lifespan. These objects are commonly used for various purposes, such as passing arguments to functions by value or returning objects from functions.

## Constructor Not Called

In most cases, the constructor of a class is called when an object is created. However, when dealing with temporary objects, the behavior is different. The C++ standard allows the compiler to optimize the creation of temporary objects, and one of the optimizations is called **copy elision**.

**Copy elision** is an optimization technique that avoids unnecessary object copying by directly constructing the destination object in its final location. This optimization is important for performance reasons, especially when dealing with large objects.

As a result of copy elision, the constructor of a temporary object may not be called. Instead, the compiler directly constructs the object in its final destination. This optimization can improve the efficiency of code execution.

## Example Code

Let's consider an example to illustrate this behavior:

```cpp
#include <iostream>

class MyClass {
public:
    MyClass() {
        std::cout << "Constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "Destructor called" << std::endl;
    }
};

void func(MyClass obj) {
    std::cout << "In function" << std::endl;
}

int main() {
    func(MyClass());
    return 0;
}
```

In this code, we have a class `MyClass` with a constructor and a destructor. The `func` function takes an object of `MyClass` as an argument.

When we call `func` with `MyClass()` as the argument, it creates a temporary object of `MyClass`. However, due to copy elision, the constructor of `MyClass` is not called explicitly for the temporary object. The compiler directly constructs the object in the function's parameter.

The output of the code will be:

```
In function
Destructor called
```

As you can see, only the destructor is called, indicating that the constructor was skipped for the temporary object.

## Conclusion

In C++, the constructor of a temporary object may not be called due to the optimization technique known as copy elision. This optimization avoids unnecessary object copying and directly constructs the object in its final location. Understanding this behavior is important when working with temporary objects and optimizing your code for performance.

#C++ #Constructors #CopyElision