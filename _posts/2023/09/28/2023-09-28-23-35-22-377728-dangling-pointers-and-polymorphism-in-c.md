---
layout: post
title: "Dangling pointers and polymorphism in C++"
description: " "
date: 2023-09-28
tags: [include, programming]
comments: true
share: true
---

Dangling pointers and polymorphism are important concepts in the C++ programming language that developers should be aware of. In this blog post, we will explore what these concepts are, how they can impact the behavior of your program, and how to avoid common pitfalls associated with them.

## Dangling Pointers

A **dangling pointer** is a pointer that points to a location in memory that has been deallocated or freed. Accessing the value at a dangling pointer can lead to undefined behavior, often resulting in crashes, segmentation faults, or data corruption.

Dangling pointers can arise in C++ in various scenarios, such as:

1. Deleting an object and accessing it using a pointer that still points to the same memory location.
2. Returning a pointer to a local variable from a function.
3. Using a pointer after the object it points to has gone out of scope.

To avoid dangling pointers, follow these best practices:

- Set pointers to `nullptr` after deleting the memory they point to.
- Avoid returning pointers to local variables from functions. Instead, use references to pass values.
- Be mindful of object lifetimes and make sure pointers are not accessed when the object they point to is no longer valid.

## Polymorphism

**Polymorphism** is a fundamental feature of object-oriented programming that allows objects of different classes to be treated as objects of a common base class. This enables writing code that can work with a variety of different objects, providing flexibility and extensibility.

In C++, polymorphism is achieved through *virtual functions*. A virtual function is a function that can be overridden by derived classes, allowing them to provide their own implementation. When a virtual function is called on a base class pointer that points to a derived class object, the appropriate derived class implementation is invoked.

Here's an example to illustrate polymorphism in C++:

```cpp
#include <iostream>

class Animal {
public:
    virtual void makeSound() {
        std::cout << "Animal makes a sound" << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "Dog barks" << std::endl;
    }
};

int main() {
    Animal* animal = new Dog();
    animal->makeSound(); // Output: Dog barks

    delete animal;
    return 0;
}
```

In the example above, we have a base class `Animal` with a virtual function `makeSound()`. The derived class `Dog` overrides this function to provide its specific implementation. When we create a `Dog` object and call `makeSound()` on a base class pointer pointing to that object, the overridden function `Dog::makeSound()` is invoked.

## Conclusion

Understanding dangling pointers and polymorphism is crucial in C++. By avoiding dangling pointers and leveraging the power of polymorphism, you can write more efficient, flexible, and bug-free code. By following best practices and being mindful of object lifetimes, you can minimize the risk of dangling pointers. And by using virtual functions, you can achieve polymorphism and design more extensible and maintainable code.

#programming #C++