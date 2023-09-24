---
layout: post
title: "Polymorphism and `std::shared_ptr`"
description: " "
date: 2023-09-24
tags: [include, include]
comments: true
share: true
---

One common challenge when working with polymorphic objects is managing their memory. This is where `std::shared_ptr` comes in handy. It is a smart pointer provided by the C++ Standard Library that helps with automatic memory management.

To understand how `std::shared_ptr` can be used with polymorphism, let's consider a simple example. Suppose we have a base class called `Shape` and two derived classes, `Circle` and `Rectangle`. `Shape` has a pure virtual function called `draw()` that must be implemented by each derived class.

```cpp
class Shape {
public:
    virtual void draw() = 0;
};

class Circle : public Shape {
public:
    void draw() override {
        // Draw a circle on the screen
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        // Draw a rectangle on the screen
    }
};
```

Now, let's say we want to create a collection of shapes and store them in a vector. Instead of directly storing objects of the derived classes in the vector, we can utilize `std::shared_ptr` to manage their memory. This way, we can easily add or remove shapes without worrying about memory leaks.

```cpp
#include <vector>
#include <memory>

int main() {
    std::vector<std::shared_ptr<Shape>> shapes;

    shapes.push_back(std::make_shared<Circle>());
    shapes.push_back(std::make_shared<Rectangle>());

    for (const auto& shape : shapes) {
        shape->draw();
    }

    return 0;
}
```

In this example, we create `shared_ptr` objects using the `make_shared` function, which takes care of allocating memory for the objects and returns a `shared_ptr` to them. The vector `shapes` stores these `shared_ptr` objects, which ensures that the memory for the objects is automatically freed when they are no longer needed.

The usage of `std::shared_ptr` ensures that the objects are correctly managed, even if we add more shapes dynamically or remove shapes from the collection. Furthermore, it allows us to call the polymorphic `draw()` function on each shape, which will execute the appropriate implementation based on the actual type of the object.

In conclusion, polymorphism and `std::shared_ptr` are powerful tools in C++ programming. By leveraging polymorphism, you can write more flexible and extensible code. And by using `std::shared_ptr`, you can ensure that the memory of polymorphic objects is properly managed, avoiding memory leaks and simplifying memory management in your applications.

#C++ #Polymorphism #SharedPtr