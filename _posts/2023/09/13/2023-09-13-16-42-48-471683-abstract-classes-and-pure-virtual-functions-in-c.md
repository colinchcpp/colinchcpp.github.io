---
layout: post
title: "Abstract classes and pure virtual functions in C++"
description: " "
date: 2023-09-13
tags: [AbstractClasses]
comments: true
share: true
---

In object-oriented programming, abstract classes and pure virtual functions play a crucial role in creating a blueprint for classes and enforcing certain behaviors. Let's dive into what abstract classes and pure virtual functions are and how they can be used in C++.

## Abstract Classes

An abstract class in C++ is a class that cannot be instantiated. It is designed to be used as a base class for other classes, providing a common interface. This allows for a level of abstraction and forces derived classes to implement certain methods.

To create an abstract class, you need to declare at least one pure virtual function. A pure virtual function is a virtual function that is declared with the `= 0` syntax at the end of its declaration. Here is an example of an abstract class:

```cpp
class Animal {
public:
    virtual void makeSound() = 0; // pure virtual function

    void sleep() {
        // implementation
    }
};
```

In this example, the `makeSound()` function is a pure virtual function, making `Animal` an abstract class. The derived classes are required to provide an implementation for this function.

## Derived Classes

Derived classes inherit from the abstract class and are responsible for implementing the pure virtual functions. They can also inherit any non-pure virtual functions and variables defined in the abstract class.

Here's an example of a derived class `Cat` that extends the `Animal` abstract class:

```cpp
class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "Meow!" << std::endl;
    }
};
```

In this example, the `Cat` class implements the `makeSound()` function defined in the `Animal` abstract class. The `override` keyword is used to indicate that we are overriding a virtual function from the base class.

## Using Abstract Classes

Abstract classes are often used as interfaces to define a common set of methods that derived classes should implement. This allows for polymorphism and enables objects of different classes to be treated interchangeably.

```cpp
void makeAnimalSound(Animal* animal) {
    animal->makeSound();
}

int main() {
    Cat cat;
    makeAnimalSound(&cat); // Output: Meow!
    return 0;
}
```

In this example, the `makeAnimalSound()` function takes a pointer to an `Animal` object and calls the `makeSound()` function. By passing a `Cat` object, which is a derived class of `Animal`, the appropriate implementation of the function is invoked.

## Conclusion

Abstract classes and pure virtual functions are powerful features of C++ that aid in creating modular and extensible code. Abstract classes provide a blueprint for derived classes, enforcing the implementation of specific methods. By utilizing abstract classes and polymorphism, we can write more flexible and maintainable code. #C++ #AbstractClasses