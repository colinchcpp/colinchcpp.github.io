---
layout: post
title: "Constructors for Factory Patterns in C++"
description: " "
date: 2023-09-23
tags: [Cplusplus]
comments: true
share: true
---

When implementing the Factory Pattern in C++, constructors play an essential role in creating objects of different types. The Factory Pattern provides an interface for creating objects, but the actual creation of objects is delegated to subclasses. This allows for flexible object creation without the need to specify the exact class of the object being created.

To implement the Factory Pattern, you need to define a base class with a virtual constructor. This base class will act as the interface for creating objects of different types. Each subclass will then implement its own version of the constructor, allowing for the creation of objects specific to that subclass.

Here's an example of how constructors for the Factory Pattern can be implemented in C++:

```cpp
#include <iostream>

// Base class with virtual constructor
class Product {
public:
    virtual ~Product() = default;
    virtual void info() = 0;
};

// Subclass A with its own constructor
class ConcreteProductA : public Product {
public:
    ConcreteProductA() {
        std::cout << "Creating ConcreteProductA" << std::endl;
    }
    void info() override {
        std::cout << "This is ConcreteProductA" << std::endl;
    }
};

// Subclass B with its own constructor
class ConcreteProductB : public Product {
public:
    ConcreteProductB() {
        std::cout << "Creating ConcreteProductB" << std::endl;
    }
    void info() override {
        std::cout << "This is ConcreteProductB" << std::endl;
    }
};

// Factory class to create objects
class Factory {
public:
    static Product* createProduct(const std::string& type) {
        // Create object based on type
        if (type == "A") {
            return new ConcreteProductA();
        } else if (type == "B") {
            return new ConcreteProductB();
        }

        return nullptr;
    }
};

int main() {
    // Create product A
    Product* productA = Factory::createProduct("A");
    productA->info();
    delete productA;

    // Create product B
    Product* productB = Factory::createProduct("B");
    productB->info();
    delete productB;

    return 0;
}
```

In the code above, we have a base class `Product` with a virtual destructor and a pure virtual function `info()`. The subclasses `ConcreteProductA` and `ConcreteProductB` each have their own constructors, where specific creation logic can be implemented.

The `Factory` class acts as a factory and has a `createProduct()` static member function. This function takes a string representing the type of product to create. Based on the provided type, it creates the corresponding object and returns a pointer to the base class `Product`.

In the `main()` function, we demonstrate the usage of the Factory Pattern by creating objects of different types using the `createProduct()` function.

Remember to hashtag your post with #Cplusplus #FactoryPattern to make it more visible to users interested in C++ and Factory Pattern discussions.