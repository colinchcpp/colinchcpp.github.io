---
layout: post
title: "Polymorphism and runtime binding in C++"
description: " "
date: 2023-09-13
tags: [Polymorphism]
comments: true
share: true
---

Polymorphism is a key feature in object-oriented programming that allows different objects to be treated as the same type. C++ supports polymorphism through the use of virtual functions and runtime binding.

## Virtual Functions

In C++, a virtual function is a member function that can be overridden by derived classes. It allows the function call to be resolved at runtime based on the actual type of the object.

To define a virtual function, we precede the function declaration in the base class with the `virtual` keyword. For example:

```cpp
class Shape {
public:
    virtual void draw() {
        // implementation specific to Shape
    }
};

class Circle : public Shape {
public:
    void draw() override {
        // implementation specific to Circle
    }
};

class Square : public Shape {
public:
    void draw() override {
        // implementation specific to Square
    }
};
```

In the above example, the `draw()` function is declared as a virtual function in the base class `Shape`. The derived classes `Circle` and `Square` override this function, providing their own specific implementations.

## Runtime Binding

Runtime binding allows the correct function to be called at runtime based on the actual object type. This is achieved through the use of pointers or references to the base class.

```cpp
void drawShape(Shape* shape) {
    shape->draw(); // Calls the appropriate draw() function based on the actual object type
}

int main() {
    Circle circle;
    Square square;

    drawShape(&circle); // Calls the draw() function specific to Circle
    drawShape(&square); // Calls the draw() function specific to Square

    return 0;
}
```

In the above example, the `drawShape()` function takes a pointer to a `Shape` object. At runtime, the correct `draw()` function is called based on the actual type of the object pointed to. This is achieved through **runtime binding**, ensuring that the appropriate function is invoked based on the object's type.

#C++ #Polymorphism