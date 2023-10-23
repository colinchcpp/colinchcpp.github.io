---
layout: post
title: "Uniform initialization with inheritance in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, inheritance is a powerful feature that allows you to create new classes based on existing ones. With the introduction of uniform initialization in C++11, initializing objects has become more consistent and intuitive. In this blog post, we will explore how uniform initialization works with inheritance in C++.

## Table of Contents
- [Introduction](#introduction)
- [Uniform Initialization](#uniform-initialization)
- [Inheritance and Uniform Initialization](#inheritance-and-uniform-initialization)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

Before diving into uniform initialization, let's quickly revisit inheritance in C++. Inheritance enables a class to inherit properties (data members and member functions) from another class, also known as the base or parent class. The derived or child class can then add its own unique properties or override inherited members.

## Uniform Initialization

Uniform initialization, introduced in C++11, provides a consistent syntax for initializing objects using braces `{}`. It allows you to initialize objects in a more intuitive and uniform way, regardless of whether they are fundamental types, user-defined types, or containers.

Here's an example of uniform initialization:

```cpp
int x{42};  // initializing an integer variable
std::vector<int> numbers{1, 2, 3, 4, 5};  // initializing a vector with values
```

Uniform initialization not only simplifies object initialization but also prevents narrowing conversions and initialization ambiguities.

## Inheritance and Uniform Initialization

When it comes to inheritance, uniform initialization works seamlessly for both base and derived classes. To initialize objects of derived classes, you can use the same uniform initialization syntax as for base classes.

Consider the following example:

```cpp
class Base {
public:
    int baseValue;
};

class Derived : public Base {
public:
    int derivedValue;
};

Derived obj{42, 24};
```

In this example, we have a base class `Base` with a single `baseValue` member, and a derived class `Derived` that inherits from `Base` and adds an additional `derivedValue` member.

We can use uniform initialization to create an object of the derived class `Derived` and initialize both `baseValue` and `derivedValue` using braces `{}`.

## Conclusion

Uniform initialization in C++ provides a cleaner and more consistent syntax for object initialization. It simplifies the process of initializing objects, whether they are base or derived classes. By utilizing uniform initialization, you can ensure code clarity and prevent potential initialization ambiguities.

In this blog post, we explored how uniform initialization works in conjunction with inheritance in C++. We saw examples of initializing objects of both base and derived classes using uniform initialization syntax. By leveraging this feature, you can enhance the readability and maintainability of your code.

## References
- [C++ Documentation - Uniform Initialization](https://en.cppreference.com/w/cpp/language/aggregate_initialization)
- [C++ Inheritance Tutorial](https://www.geeksforgeeks.org/inheritance-in-c/)