---
layout: post
title: "Introduction to C++ OOP concepts"
description: " "
date: 2023-09-13
tags: []
comments: true
share: true
---

## Understanding Classes and Objects

At the core of OOP in C++ are classes and objects. A **class** is a blueprint for creating objects. It defines the properties (attributes or data fields) and behaviors (methods or member functions) that the objects of that class will have.

An **object** is an instance of a class. It represents a specific entity, such as a person, car, or bank account, and holds its own unique set of data and behaviors defined by the class.

Here's an example of a class in C++:

```cpp
class Car {
public:
    // attributes
    string color;
    string brand;
    int year;
    
    // methods
    void startEngine() {
        cout << "Engine started!" << endl;
    }
    
    void stopEngine() {
        cout << "Engine stopped!" << endl;
    }
};
```

## Encapsulation, Inheritance, and Polymorphism

One of the key principles of OOP is **encapsulation**, which is the bundling of data and methods that operate on that data into a single unit (i.e., class). This encapsulation ensures data integrity and provides abstraction, allowing us to hide the internal implementation details.

Another important concept is **inheritance**, which allows a class to inherit the properties and behaviors of another class. This promotes code reuse and allows for the creation of more specialized classes based on a common base class.

The concept of **polymorphism** allows objects of different classes to be treated as objects of a common base class. This enables us to write more generic code that can work with objects of different types, providing flexibility and extensibility to our programs.

## C++ OOP Example

Let's take a look at an example that showcases these concepts:

```cpp
class Shape {
public:
    virtual float area() = 0; // pure virtual function

    void displayArea() {
        cout << "Area: " << area() << " square units" << endl;
    }
};

class Rectangle : public Shape {
private:
    float length;
    float width;

public:
    Rectangle(float length, float width) {
        this->length = length;
        this->width = width;
    }

    float area() {
        return length * width;
    }
};

class Circle : public Shape {
private:
    float radius;

public:
    Circle(float radius) {
        this->radius = radius;
    }

    float area() {
        return 3.14 * radius * radius;
    }
};

int main() {
    Rectangle rect(5, 10);
    Circle circle(7);

    rect.displayArea();
    circle.displayArea();

    return 0;
}
```

In this example, we have a base class `Shape` with a pure virtual function `area()`. We then derive two subclasses `Rectangle` and `Circle` from `Shape` and provide their own implementation of the `area()` function. The `displayArea()` function demonstrates polymorphism by calling the appropriate `area()` implementation based on the object type.

## Conclusion

In this blog post, we have covered the basics of object-oriented programming in C++. We explored the concepts of classes, objects, encapsulation, inheritance, and polymorphism. Understanding and applying these concepts will not only help you write more modular and reusable code but also enhance your overall programming skills. Happy coding!

#C++ #OOP