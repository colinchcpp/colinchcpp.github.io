---
layout: post
title: "Functors and polymorphism in C++: an in-depth comparison"
description: " "
date: 2023-09-14
tags: [Functors, Polymorphism]
comments: true
share: true
---

In the world of C++, functors and polymorphism are powerful concepts that allow developers to write more flexible and reusable code. While they both serve similar purposes, there are some key differences between the two. In this blog post, we'll take an in-depth look at functors and polymorphism in C++ and discuss when to use each of them.

## Functors

Let's start with functors. In C++, a functor is simply an object that can be called like a function. It overloads the `operator()` which allows the object to be invoked using the function call syntax. Functors can be useful in scenarios where we need to encapsulate some logic and pass it around as a parameter.

### Creating a Functor

To create a functor in C++, we define a class with an overloaded `operator()` method. Here's an example of a simple functor that multiplies two integers:

```cpp
class Multiplier {
public:
    int operator()(int a, int b) const {
        return a * b;
    }
};
```

We can now create an instance of this functor and use it like a regular function:

```cpp
Multiplier multiply;
int result = multiply(5, 4); // 20
```

### Benefits of Functors

Functors provide a level of abstraction that allows us to pass behavior as parameters. This makes them particularly useful in scenarios where we need to customize the behavior of a function or algorithm. They are also more efficient compared to function pointers since functors can be inlined by the compiler.

## Polymorphism

Polymorphism, on the other hand, is a fundamental concept in object-oriented programming that allows objects of different types to be treated as instances of a common base class. It enables code to be written in a more generic way, allowing for flexibility and extensibility.

### Creating a Polymorphic Hierarchy

To illustrate polymorphism, let's create a simple example using a base class `Shape` and its derived classes `Circle` and `Rectangle`:

```cpp
class Shape {
public:
    virtual double area() const = 0;
};

class Circle : public Shape {
    double radius;
public:
    Circle(double radius) : radius(radius) {}
    double area() const override {
        return 3.14159 * radius * radius;
    }
};

class Rectangle : public Shape {
    double width;
    double height;
public:
    Rectangle(double width, double height) : width(width), height(height) {}
    double area() const override {
        return width * height;
    }
};
```

In the example above, `Shape` is an abstract base class with a pure virtual `area()` function. The derived classes, `Circle` and `Rectangle`, implement the `area()` function according to their respective formulas.

### Polymorphic Usage

Using polymorphism, we can treat objects of derived classes as instances of the base class. Here's an example of how we can calculate the areas of shapes stored in a vector:

```cpp
std::vector<std::unique_ptr<Shape>> shapes;
shapes.push_back(std::make_unique<Circle>(5.0));
shapes.push_back(std::make_unique<Rectangle>(4.0, 6.0));

for (const auto& shape : shapes) {
    double area = shape->area();
    std::cout << "Area: " << area << std::endl;
}
```

The code above demonstrates how polymorphism allows us to iterate over a collection of different shapes and call the `area()` function without knowing the specific derived type. This flexibility and extensibility make polymorphism a powerful tool in C++.

## Conclusion

Functors and polymorphism are both important concepts in C++ that serve similar purposes but with different approaches. Functors provide a way to encapsulate logic and pass it around as parameters, while polymorphism allows objects of different types to be treated as instances of a common base class. Understanding the differences and use cases of functors and polymorphism can greatly improve your C++ programming skills.

#C++ #Functors #Polymorphism