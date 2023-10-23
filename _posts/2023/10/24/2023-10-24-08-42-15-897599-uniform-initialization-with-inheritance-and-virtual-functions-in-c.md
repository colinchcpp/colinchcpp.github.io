---
layout: post
title: "Uniform initialization with inheritance and virtual functions in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, uniform initialization allows you to initialize objects using a consistent syntax, regardless of whether they are built-in types, user-defined types, or derived from base classes. This feature becomes particularly useful when working with inheritance and virtual functions.

## Inheriting from a base class

To demonstrate uniform initialization with inheritance, let's first consider a simple example of a base class called `Shape`, which has a virtual function `draw()`:

```cpp
class Shape {
public:
    virtual void draw() const = 0;
};
```

Now, let's create a derived class called `Circle` that inherits from `Shape`:

```cpp
class Circle : public Shape {
private:
    int radius;

public:
    void draw() const override {
        // Implement the drawing logic for Circle
    }
};
```

## Uniform initialization of derived classes

With uniform initialization, you can easily initialize objects of derived classes and pass arguments to their constructors using a concise syntax. Here's an example of how you can create an instance of the `Circle` class:

```cpp
Circle circle{10}; // Initialize a Circle object with radius 10
```

In this example, the constructor of the `Circle` class takes an `int` argument, which represents the radius of the circle. By using uniform initialization with curly braces, we can pass the value `10` directly to the constructor.

## Using virtual functions

Virtual functions allow derived classes to override the behavior of base class functions. This means that when calling a virtual function on a base class pointer or reference, the overridden function in the derived class will be executed.

To illustrate this, let's assume we have a vector of base class pointers, where we store instances of different derived classes:

```cpp
std::vector<Shape*> shapes;
shapes.push_back(new Circle{5});  // Add a Circle object to the vector
```

We can then iterate over the vector and call the `draw()` function on each object. The appropriate `draw()` implementation from the derived class will be invoked:

```cpp
for (const auto& shape : shapes) {
    shape->draw();  // Calls the draw() function of the respective derived class
}
```

This code snippet demonstrates the power of virtual functions combined with uniform initialization. It allows us to easily create and manipulate objects of derived classes, while still ensuring that the correct overridden functions are called.

## Conclusion

Uniform initialization provides a consistent way to initialize objects, including derived classes, in C++. This feature becomes especially useful when working with inheritance and virtual functions, as it simplifies object creation and method invocation. By leveraging uniform initialization and virtual functions, you can write clean and elegant code that is easy to read and maintain.

#### References:
- [C++ Documentation: Uniform initialization](https://en.cppreference.com/w/cpp/language/uniform_initialization)
- [C++ Documentation: Virtual functions](https://en.cppreference.com/w/cpp/language/virtual)