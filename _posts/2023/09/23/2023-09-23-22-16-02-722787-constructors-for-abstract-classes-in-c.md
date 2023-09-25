---
layout: post
title: "Constructors for Abstract Classes in C++"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In C++, an abstract class is a class that provides a common interface for its derived classes but cannot be instantiated itself. Abstract classes are useful when you want to define a base class with some common functionality, but want to enforce that its derived classes provide specific implementations for some methods.

One important aspect of abstract classes is the use of constructors. While it may seem counterintuitive to have constructors in abstract classes, they serve an important purpose. Constructors in abstract classes can be used to initialize the common data members that are shared by all derived classes.

When defining constructors for an abstract class, consider the following guidelines:

1. Constructors can be declared in the abstract class just like any other member function, but they cannot be directly called or instantiated.
2. In most cases, constructors for abstract classes are declared as protected. This prevents direct instantiation of the abstract class but allows derived classes to access and invoke the constructor during their own initialization process.
3. Constructors in abstract classes can be used to initialize the data members that are common to all derived classes. These common data members can be declared and defined in the abstract class itself.

Here's an example that demonstrates the usage of constructors in an abstract class:

```cpp
#include<iostream>
using namespace std;

// Abstract class
class Shape {
protected:
    int x, y; // Common data members
    
    // Protected constructor
    Shape(int x, int y): x(x), y(y) {}
    
public:
    // Abstract method
    virtual void draw() = 0;
};

// Derived classes
class Circle : public Shape {
public:
    // Constructor calls the base class constructor
    Circle(int x, int y) : Shape(x, y) {}
    
    // Implementing the draw method
    void draw() {
        cout << "Drawing a circle at (" << x << ", " << y << ")" << endl;
    }
};

class Square : public Shape {
public:
    // Constructor calls the base class constructor
    Square(int x, int y) : Shape(x, y) {}
    
    // Implementing the draw method
    void draw() {
        cout << "Drawing a square at (" << x << ", " << y << ")" << endl;
    }
};

int main() {
    // Cannot instantiate abstract class Shape
    // Shape shape; 
    
    // Creating objects of derived classes
    Circle circle(5, 10);
    Square square(15, 20);
    
    // Calling the draw method on objects
    circle.draw();
    square.draw();
    
    return 0;
}
```
In the example above, we have an abstract class called `Shape` that has two common data members `x` and `y`. The constructor `Shape(int x, int y)` initializes these data members and is declared as protected. We then have two derived classes, `Circle` and `Square`, which inherit from the `Shape` class. These derived classes call the base class constructor `Shape(x, y)` during their own initialization. Each derived class provides its own implementation of the `draw()` method.

To summarize, constructors in abstract classes are used to initialize common data members and are typically declared as protected. Derived classes can call the base class constructor to initialize the common data members during their own initialization process.