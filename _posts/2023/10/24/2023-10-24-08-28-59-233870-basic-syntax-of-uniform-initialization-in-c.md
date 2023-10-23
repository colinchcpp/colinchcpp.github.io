---
layout: post
title: "Basic syntax of uniform initialization in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Uniform initialization is a syntax introduced in C++11 to simplify and make the initialization of objects more consistent. It provides a consistent way to initialize objects using parentheses `{}`. In this blog post, we will explore the basic syntax and usage of uniform initialization in C++.

## Table of Contents

- [Introduction](#introduction)
- [Syntax](#syntax)
- [Examples](#examples)
- [Benefits](#benefits)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

Prior to C++11, there were multiple ways to initialize objects: direct initialization, copy initialization, and value initialization. These different approaches led to inconsistencies and confusion. Uniform Initialization introduced a single, consistent way to initialize objects using braces `{}`.

## Syntax

The basic syntax of uniform initialization is as follows:

```cpp
T object {initializers};
```

Here, `T` is the type of the object being initialized, `object` is the name of the object, and `initializers` are the values used for initialization. It is important to note that if the type `T` has an initializer-list constructor, it will be preferred over other constructors.

Uniform initialization can be used with the following types:

- Fundamental types
- User-defined types
- Arrays
- Standard library containers
- Aggregate types

## Examples

Let's look at some examples to understand how uniform initialization works:

### Initializing a Fundamental Type

```cpp
int num1{10};
int num2 = {20};

double pi{3.14};
double e = {2.71};
```

### Initializing a User-Defined Type

```cpp
class Point {
public:
    int x;
    int y;
};
Point p1{1, 2};
Point p2 = {3, 4};
```

### Initializing an Array

```cpp
int arr1[3] {1, 2, 3};
int arr2[] = {4, 5, 6};
```

### Initializing a Standard Library Container

```cpp
std::vector<int> vec1 {1, 2, 3};
std::vector<int> vec2 = {4, 5, 6};
```

### Initializing an Aggregate Type

```cpp
struct Rectangle {
    int width;
    int height;
};

Rectangle rect1 {10, 20};
Rectangle rect2 = {30, 40};
```

## Benefits

Uniform initialization provides several benefits:

1. Consistency: It offers a consistent and straightforward syntax for all types of initialization.
2. Prevention of narrowing conversions: It allows the detection of narrowing conversions during compilation, preventing loss of data and narrowing errors.
3. Prevention of most vexing parse: It avoids accidental function declarations when declaring objects without initialization.
4. Improved readability and maintainability: The use of braces `{}` explicitly indicates initialization and makes the code more readable and understandable.

## Conclusion

Uniform initialization is a powerful feature introduced in C++11 that simplifies and makes the initialization of objects more consistent. It offers a single, consistent syntax for all types of initialization, preventing narrowing conversions and most vexing parse errors. By using uniform initialization, you can write more readable and maintainable code.

## References

- [C++11 Uniform Initialization](https://en.cppreference.com/w/cpp/language/initializer_list)
- [C++11 Initialization](https://www.geeksforgeeks.org/initialization-of-non-static-members-in-c/)
- [Effective Modern C++ by Scott Meyers](https://www.oreilly.com/library/view/effective-modern-c/9781491908419/)
- [C++ Primer by Stanley Lippman, Josee Lajoie, and Barbara E. Moo](https://www.oreilly.com/library/view/c-primer-fifth/9780133053035/)