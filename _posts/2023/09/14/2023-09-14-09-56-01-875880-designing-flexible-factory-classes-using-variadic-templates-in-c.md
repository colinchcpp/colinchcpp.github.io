---
layout: post
title: "Designing flexible factory classes using variadic templates in C++"
description: " "
date: 2023-09-14
tags: [include, include, include, include, VariadicTemplates, FactoryDesignPattern]
comments: true
share: true
---

## Introduction

In object-oriented programming, the factory design pattern is commonly used to create objects without exposing the instantiation logic to the client. However, the traditional implementation of the factory pattern can become cumbersome when working with a large number of product types. 

In this article, we will explore how we can leverage variadic templates in C++ to design flexible factory classes that can handle an arbitrary number of product types.

## The problem with traditional factory classes

Traditional factory classes typically use a mapping between product names and concrete product types, often implemented using conditional statements or switch-case constructs. This approach can quickly become bloated and difficult to maintain when dealing with a large number of product types.

Here's an example of a traditional factory class for creating different types of shapes:

```cpp
#include <iostream>
#include <memory>

enum class ShapeType {
    Circle,
    Rectangle,
    Triangle
};

class Shape {
public:
    virtual void draw() = 0;
    virtual ~Shape() {}
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Rectangle" << std::endl;
    }
};

class Triangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Triangle" << std::endl;
    }
};

class ShapeFactory {
public:
    std::unique_ptr<Shape> createShape(ShapeType type) {
        switch (type) {
            case ShapeType::Circle:
                return std::make_unique<Circle>();
            case ShapeType::Rectangle:
                return std::make_unique<Rectangle>();
            case ShapeType::Triangle:
                return std::make_unique<Triangle>();
            default:
                return nullptr;
        }
    }
};

int main() {
    ShapeFactory factory;
    
    auto circle = factory.createShape(ShapeType::Circle);
    circle->draw();

    auto rectangle = factory.createShape(ShapeType::Rectangle);
    rectangle->draw();

    auto triangle = factory.createShape(ShapeType::Triangle);
    triangle->draw();

    return 0;
}
```

As you can see, adding new shape types would require modifying the factory class and adding new cases to the switch statement. This approach violates the open-closed principle and makes the code less flexible and maintainable.

## Introducing variadic templates

Variadic templates are a feature in C++ that allows us to define functions or classes that can accept an arbitrary number of template arguments. By leveraging variadic templates, we can create a flexible factory class that is capable of handling any number of product types without modifying the class itself.

Let's reimplement the shape factory using variadic templates:

```cpp
#include <iostream>
#include <memory>

enum class ShapeType {
    Circle,
    Rectangle,
    Triangle
};

class Shape {
public:
    virtual void draw() = 0;
    virtual ~Shape() {}
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Rectangle" << std::endl;
    }
};

class Triangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Triangle" << std::endl;
    }
};

template<typename... ShapeTypes>
class ShapeFactory {
public:
    template<typename ShapeType>
    std::unique_ptr<Shape> createShape() {
        if constexpr ((std::is_same_v<ShapeType, ShapeTypes> || ...)) {
            return std::make_unique<ShapeType>();
        }
        else {
            return nullptr;
        }
    }
};

int main() {
    ShapeFactory<Circle, Rectangle, Triangle> factory;
    
    auto circle = factory.createShape<Circle>();
    circle->draw();

    auto rectangle = factory.createShape<Rectangle>();
    rectangle->draw();

    auto triangle = factory.createShape<Triangle>();
    triangle->draw();

    return 0;
}
```

In the updated implementation, we use a variadic template class that takes any number of shape types as template arguments. The `createShape` function makes use of constexpr and fold expressions to check if the provided shape type matches any of the template arguments.

By using variadic templates, we achieve a more flexible and extensible factory class that doesn't require modifying the class itself when adding new shape types.

## Conclusion

Variadic templates provide a powerful tool for designing flexible factory classes in C++. By leveraging variadic templates, we can create factories that can handle an arbitrary number of product types without sacrificing flexibility and maintainability.

With the implementation using variadic templates, adding new product types becomes a breeze and doesn't require modifying the factory class itself. This allows us to follow the open-closed principle and makes our code more extensible. 

So next time you need to implement factories in C++, consider using variadic templates to achieve a more flexible and scalable solution.

#C++ #VariadicTemplates #FactoryDesignPattern