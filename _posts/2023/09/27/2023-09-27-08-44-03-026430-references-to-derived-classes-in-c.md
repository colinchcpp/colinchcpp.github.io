---
layout: post
title: "References to derived classes in C++"
description: " "
date: 2023-09-27
tags: [DerivedClasses]
comments: true
share: true
---

In C++, a derived class is a class that is derived from another class, known as the base class. Derived classes inherit the properties and behavior of the base class, and you can use references to access objects of derived classes in a variety of ways. Let's explore some common scenarios for referencing derived classes in C++.

## 1. Base Class Pointers

You can use a base class pointer to refer to objects of both the base class and its derived classes. This is possible because a derived class is a specialized version of its base class. Here's an example:

```cpp
class Shape {
public:
    virtual void draw() {
        cout << "Drawing a shape" << endl;
    }
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle" << endl;
    }
};

int main() {
    Shape* shapePtr;

    Circle circle;
    shapePtr = &circle;

    shapePtr->draw(); // Outputs "Drawing a circle"
}
```

In this example, we define a base class `Shape` and a derived class `Circle`. We create a pointer of type `Shape*` and assign it the address of the `Circle` object. When we call the `draw()` method, the derived class implementation is invoked, even though we are using a base class pointer.

## 2. Object Slicing

When assigning a derived class object to a base class object, object slicing occurs. Object slicing refers to the loss of derived class-specific information when storing an object in a base class container. Here's an example:

```cpp
class Animal {
public:
    virtual void makeSound() {
        cout << "Animal sound" << endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        cout << "Meow" << endl;
    }
};

int main() {
    Animal animal = Cat();
    animal.makeSound(); // Outputs "Animal sound"
}
```

In this example, we create a base class `Animal` and a derived class `Cat`. When we assign a `Cat` object to an `Animal` object, **object slicing** occurs. As a result, only the base class information is retained, and the derived class-specific behavior is lost.

## Conclusion

Referencing derived classes in C++ is an essential aspect of object-oriented programming. By using base class pointers, you can work with objects of derived classes while maintaining flexibility and polymorphism. However, it's important to be aware of object slicing, which can lead to the loss of derived class-specific information when assigning objects to base class containers.

Remember to utilize these concepts effectively in your C++ programs to harness the power of inheritance and polymorphism.

#C++ #DerivedClasses