---
layout: post
title: "Exploring the concept of 'friend' classes in operator overloading in C++"
description: " "
date: 2023-09-14
tags: [cplusplus, operators]
comments: true
share: true
---

## Introduction

In C++, the concept of operator overloading allows us to redefine the functionality of existing operators to work with user-defined data types. This powerful feature helps to make our code more expressive and concise. However, there are cases where our custom operators need access to private members of another class. In such situations, the `friend` keyword comes to the rescue.

## What are 'friend' classes?

In C++, a `friend` class is a class that is granted access to the private and protected members of another class. This allows the `friend` class to access and modify the private data of the class it is declared as a friend of. In the context of operator overloading, declaring a class as a `friend` gives it the ability to access private members while overloading an operator.

## Example

Let's consider a simplified example where we have a `Point` class representing a point in 2D Cartesian coordinates, and we want to overload the addition operator (`+`) to add two `Point` objects together.

Here's the implementation of the `Point` class:

```cpp
class Point {
private:
    int x, y;

public:
    Point(int x, int y) : x(x), y(y) {}

    friend Point operator+(const Point& p1, const Point& p2) {
        return Point(p1.x + p2.x, p1.y + p2.y);
    }
};
```

In the above code, we have declared the `operator+` function as a `friend` of the `Point` class. This allows the `operator+` function to directly access the private `x` and `y` members of both `Point` objects `p1` and `p2`.

## Usage

Now, let's see how we can use the overloaded `+` operator with our `Point` objects:

```cpp
int main() {
    Point p1(2, 3);
    Point p2(4, 5);
    Point sum = p1 + p2;

    return 0;
}
```

In the `main` function, we create two `Point` objects, `p1` and `p2`, with coordinates `(2, 3)` and `(4, 5)` respectively. We then use the overloaded `+` operator to add these two points together and assign the result to the `sum` variable.

## Conclusion

The `friend` keyword in C++ allows us to grant access to private members of a class to another class or function. Overloading operators with the help of `friend` classes enhances the flexibility of operator overloading, enabling operations on user-defined types that would otherwise be inaccessible. Understanding the concept of `friend` classes can greatly expand the capabilities of your C++ programs.

#cplusplus #operators