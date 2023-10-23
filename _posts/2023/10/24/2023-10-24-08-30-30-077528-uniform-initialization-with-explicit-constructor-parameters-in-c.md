---
layout: post
title: "Uniform initialization with explicit constructor parameters in C++"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

In modern C++, uniform initialization syntax has become the preferred way to initialize objects. It offers a concise and consistent way to initialize objects, regardless of their type. In this blog post, we will explore how to use uniform initialization with explicit constructor parameters in C++.

## What is Uniform Initialization?

Uniform initialization, introduced in C++11, provides a unified syntax for initializing objects of different types. It allows you to initialize objects using a set of curly braces `{}` or parentheses `()`.

The syntax for uniform initialization is as follows:

```cpp
Type variable{value1, value2, ...};
```

or

```cpp
Type variable(value1, value2, ...);
```

Uniform initialization can be used to initialize fundamental types, aggregate types, and class types.

## Using Uniform Initialization with Explicit Constructor Parameters

In C++, constructors can have explicit parameters defined to initialize objects. When using uniform initialization, the explicit constructor parameters can be provided inside the curly braces or parentheses.

Consider the following example:

```cpp
class Point {
public:
    explicit Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};

int main() {
    Point p1{10, 20}; // Uniform initialization using braces
    Point p2(30, 40); // Uniform initialization using parentheses
    
    std::cout << "p1: (" << p1.getX() << ", " << p1.getY() << ")" << std::endl;
    std::cout << "p2: (" << p2.getX() << ", " << p2.getY() << ")" << std::endl;
    
    return 0;
}
```

In the above example, we have a `Point` class with an explicit constructor that takes two integers as parameters. We can initialize `Point` objects `p1` and `p2` using either braces or parentheses.

When using uniform initialization, the constructor parameters are enclosed within the braces or parentheses, just like when initializing aggregate types.

## Benefits of Uniform Initialization

Using uniform initialization with explicit constructor parameters offers several benefits:

1. Consistent syntax: Uniform initialization provides a consistent syntax for initializing objects, regardless of their types. This improves code readability and reduces confusion.

2. Implicit type conversion prevention: Using explicit constructor parameters with uniform initialization helps prevent implicit type conversions. This can prevent unintended object initialization and potential bugs.

3. Narrowing conversion detection: Uniform initialization with explicit constructor parameters helps detect narrowing conversions during initialization. Narrowing conversions, such as truncation of floating-point values, can lead to unexpected results. Uniform initialization helps catch such conversions at compile-time.

## Conclusion

Uniform initialization with explicit constructor parameters in C++ provides a concise and consistent way to initialize objects. It offers numerous benefits, including a unified syntax, prevention of implicit type conversions, and detection of narrowing conversions. By leveraging uniform initialization, you can write cleaner and safer C++ code.

#References:
- [C++11 Uniform Initialization](https://en.cppreference.com/w/cpp/language/list_initialization)
- [C++ Constructor Initialization List](https://www.geeksforgeeks.org/when-do-we-use-initializer-list-in-c/)