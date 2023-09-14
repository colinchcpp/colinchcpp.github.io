---
layout: post
title: "Overloading operators for custom vector and matrix operations in C++"
description: " "
date: 2023-09-14
tags: [programming, cplusplus]
comments: true
share: true
---

Operators in C++ can be overloaded to perform custom operations on user-defined classes, such as vectors and matrices. This allows for more intuitive and natural syntax when working with these objects. In this blog post, we will explore how to overload operators for custom vector and matrix operations in C++.

## Overloading Operators for Vectors

To start, let's create a `Vector` class with two member variables: `x` and `y`. We will overload the `+` and `-` operators to add and subtract two vectors respectively.

```cpp
class Vector {
public:
    double x, y;

    Vector(double x, double y) : x(x), y(y) {}

    Vector operator+(const Vector& other) const {
        return Vector(x + other.x, y + other.y);
    }
    
    Vector operator-(const Vector& other) const {
        return Vector(x - other.x, y - other.y);
    }
};
```

Now, we can use the overloaded operators to perform vector addition and subtraction with ease:

```cpp
Vector v1(1, 2);
Vector v2(3, 4);

Vector resultAdd = v1 + v2; // resultAdd = Vector(4, 6)
Vector resultSub = v1 - v2; // resultSub = Vector(-2, -2)
```

## Overloading Operators for Matrices

Next, let's create a `Matrix` class with a 2D array to store the matrix elements. We will overload the `+` operator to add two matrices together.

```cpp
class Matrix {
public:
    int rows, cols;
    std::vector<std::vector<int>> elements;

    Matrix(int rows, int cols) : rows(rows), cols(cols) {
        elements.resize(rows, std::vector<int>(cols));
    }

    Matrix operator+(const Matrix& other) const {
        Matrix result(rows, cols);

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.elements[i][j] = elements[i][j] + other.elements[i][j];
            }
        }

        return result;
    }
};
```

We can now use the overloaded `+` operator to add two matrices together:

```cpp
Matrix m1(2, 2);
m1.elements = {{1, 2}, {3, 4}};

Matrix m2(2, 2);
m2.elements = {{5, 6}, {7, 8}};

Matrix result = m1 + m2;
```

## Conclusion

Overloading operators allows us to define custom operations for user-defined classes in C++, making the code more readable and intuitive. By overloading operators for vector and matrix operations, we can perform mathematical operations with ease. Whether it's vector addition or matrix addition, overloading operators provides a convenient way to work with these objects.

#programming #cplusplus