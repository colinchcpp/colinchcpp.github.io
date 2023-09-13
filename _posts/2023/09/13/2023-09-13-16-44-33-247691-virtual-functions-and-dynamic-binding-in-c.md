---
layout: post
title: "Virtual functions and dynamic binding in C++"
description: " "
date: 2023-09-13
tags: [polymorphism]
comments: true
share: true
---

In object-oriented programming, **polymorphism** is a powerful feature that allows objects of different classes to be treated as objects of a common parent class. One key aspect of polymorphism in C++ is the use of **virtual functions** and **dynamic binding**.

## Virtual Functions

A virtual function is a member function declared in the base class and overridden in the derived class. The keyword `virtual` is used to declare a function as virtual. This allows the function to be dynamically bound at runtime based on the actual type of the object.

Here's an example to illustrate the concept:

```cpp
class Shape {
public:
    virtual void draw() {
        // Common implementation for all shapes
    }
};

class Circle : public Shape {
public:
    void draw() override {
        // Implementation specific to a circle
    }
};

class Square : public Shape {
public:
    void draw() override {
        // Implementation specific to a square
    }
};

int main() {
    Circle circle;
    Square square;
    Shape* shapePtr;

    shapePtr = &circle;
    shapePtr->draw();  // Calls the draw() function of the Circle class

    shapePtr = &square;
    shapePtr->draw();  // Calls the draw() function of the Square class

    return 0;
}
```

In the above example, the `draw()` function is declared as virtual in the base class `Shape`. Both the derived classes `Circle` and `Square` override this function. During runtime, the `draw()` function is dynamically bound based on the actual type of the object pointed to by `shapePtr`.

## Dynamic Binding

Dynamic binding, also known as **late binding** or **run-time polymorphism**, allows the selection of the appropriate function implementation at runtime based on the actual type of the object, rather than the type of the pointer or reference to the object.

In the `main()` function of the above example, `shapePtr` is a pointer of type `Shape*`. However, it can point to objects of different derived classes (`Circle` and `Square`) that inherit from `Shape`. The `draw()` function is invoked through `shapePtr`, and the appropriate implementation is selected based on the actual type of the object.

Dynamic binding enables more flexible and extensible code, as it allows new derived classes to be added without modifying existing code that operates on the base class.

## Conclusion

Virtual functions and dynamic binding are key concepts in C++ that enable polymorphism and runtime flexibility. By using virtual functions, you can create a common interface in the base class and have different implementations in derived classes. This allows you to write more modular and scalable code, enhancing code reusability and extensibility.

#C++ #polymorphism