---
layout: post
title: "Constructor in Inheritance in C++"
description: " "
date: 2023-09-23
tags: [inheritance]
comments: true
share: true
---

In C++, inheritance allows one class (called the derived class) to inherit the properties and methods of another class (called the base class). When working with inheritance, it is essential to understand how constructors are inherited and how they can be invoked.

## Inheriting the Base Class Constructor

When a derived class is created, it automatically inherits the constructor(s) of its base class(es). The derived class constructor can then use the base class constructor to initialize the inherited members. This is done using the initialization list in the derived class constructor.

Here's an example:

```c++
// Base class
class Animal {
protected:
    std::string name;

public:
    Animal(const std::string& name) : name(name) {
        std::cout << "Animal constructor called." << std::endl;
    }
};

// Derived class
class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {
        std::cout << "Dog constructor called." << std::endl;
    }
};
```

In the example above, the `Dog` class is derived from the `Animal` class. The `Dog` constructor uses the `Animal` constructor to initialize the `name` member variable of the `Animal` class. The base class constructor is called using the `:` (colon) syntax followed by the base class name and the arguments to be passed to the base class constructor.

## Constructor Invocation in Inheritance

Inheritance allows us to create objects of the derived class, but this also means that the constructor hierarchy needs to be followed for object creation.

Consider the following example:

```c++
int main() {
    Dog dog("Buddy");

    return 0;
}
```

In this example, the `Dog` object named "Buddy" is created. When the `Dog` constructor is invoked, it first calls the `Animal` constructor to initialize the `name` member variable. The output would be:
```
Animal constructor called.
Dog constructor called.
```

By following the constructor hierarchy, we ensure that the base class members are properly initialized before the derived class constructor is executed.

## Conclusion

Constructors are inherited in C++ during class inheritance. The derived class constructor can use the base class constructor to initialize inherited members. By understanding the principles of constructor invocation in inheritance, we can ensure the proper initialization of objects in a derived class.

#cpp #inheritance