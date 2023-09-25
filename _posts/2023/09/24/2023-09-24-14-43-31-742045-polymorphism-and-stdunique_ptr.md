---
layout: post
title: "Polymorphism and `std::unique_ptr`"
description: " "
date: 2023-09-24
tags: [polymorphism]
comments: true
share: true
---

`std::unique_ptr` is a smart pointer provided by the C++ Standard Library. It is designed to provide exclusive ownership of the dynamically allocated memory while automatically managing the object destruction. It ensures that only one `std::unique_ptr` can own an object, preventing multiple ownership and resource leaks.

To understand how `std::unique_ptr` can be used in polymorphism, let's consider an example scenario where we have a base class `Shape` and two derived classes `Circle` and `Rectangle`. Here's some code to illustrate this:

```cpp
#include <memory>

class Shape {
public:
    virtual void draw() const = 0;
    virtual ~Shape() = default; // Polymorphic base class destructor
};

class Circle : public Shape {
public:
	void draw() const override {
		// Draw circle implementation
	}
};

class Rectangle : public Shape {
public:
	void draw() const override {
		// Draw rectangle implementation
	}
};

int main() {
    std::unique_ptr<Shape> shape1 = std::make_unique<Circle>();
    std::unique_ptr<Shape> shape2 = std::make_unique<Rectangle>();

    shape1->draw(); // Calls draw() of Circle class
    shape2->draw(); // Calls draw() of Rectangle class

    return 0;
}
```

In this example, we define the base class `Shape` with a pure virtual function `draw()`. The derived classes `Circle` and `Rectangle` inherit from `Shape` and provide their own implementation of the `draw()` function.

Inside the `main()` function, we create `std::unique_ptr` objects with the base class type and assign them to instances of the derived classes. This demonstrates how `std::unique_ptr` can be used to manage polymorphic objects. The `draw()` function is invoked on each `std::unique_ptr` object using the arrow operator (`->`), which automatically dispatches to the appropriate derived class implementation.

By using `std::unique_ptr` with polymorphism, we ensure that the memory allocated for each object is automatically released when the pointer goes out of scope. It eliminates the need for manual memory management and helps prevent memory leaks, which is especially important when dealing with polymorphic objects.

In conclusion, `std::unique_ptr` is a valuable tool when it comes to managing polymorphic objects in C++. It provides automatic memory management and ensures the correct destruction of objects. Leveraging the power of polymorphism with `std::unique_ptr` leads to cleaner, safer, and more maintainable code. #polymorphism #stduniqueptr