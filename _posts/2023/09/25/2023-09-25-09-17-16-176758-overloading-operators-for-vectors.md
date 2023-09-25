---
layout: post
title: "Overloading operators for vectors"
description: " "
date: 2023-09-25
tags: [vector]
comments: true
share: true
---

In object-oriented programming, operator overloading allows us to define how operators, such as +, -, *, /, and ==, work with custom objects. This enables us to use familiar syntax when working with our own classes.

In this blog post, we will discuss how to overload operators specifically for vectors. Imagine we have a `Vector` class that represents a mathematical vector with x, y, and z components.

## Addition and Subtraction

When dealing with vectors, it is common to perform addition and subtraction to combine or separate vectors. To enable this, we can overload the `+` and `-` operators.

```cpp
class Vector {
    float x, y, z;

public:
    Vector(float x, float y, float z) : x(x), y(y), z(z) {}

    Vector operator+(const Vector& other) const {
        return Vector(x + other.x, y + other.y, z + other.z);
    }

    Vector operator-(const Vector& other) const {
        return Vector(x - other.x, y - other.y, z - other.z);
    }
};
```

Now, we can add or subtract `Vector` objects using the familiar `+` and `-` operators:

```cpp
Vector v1(1, 2, 3);
Vector v2(4, 5, 6);
Vector result = v1 + v2;  // (5, 7, 9)
Vector result2 = v2 - v1; // (3, 3, 3)
```

## Scalar Multiplication

Multiplying a vector by a scalar value is another common operation in vector mathematics. We can overload the `*` operator to perform this operation.

```cpp
class Vector {
    // ...

public:
    // ...

    Vector operator*(float scalar) const {
        return Vector(x * scalar, y * scalar, z * scalar);
    }
};
```

Now, we can scale a `Vector` object by a scalar value using the `*` operator:

```cpp
Vector v1(1, 2, 3);
Vector scaled = v1 * 2; // (2, 4, 6)
```

## Equality Comparison

Checking whether two vectors are equal is another important operation. We can overload the `==` operator to compare two `Vector` objects.

```cpp
class Vector {
    // ...

public:
    // ...

    bool operator==(const Vector& other) const {
        return (x == other.x) && (y == other.y) && (z == other.z);
    }
};
```

Now, we can check for equality between two `Vector` objects using the `==` operator:

```cpp
Vector v1(2, 3, 4);
Vector v2(2, 3, 4);
if (v1 == v2) {
    // Do something
}
```

## Conclusion

Overloading operators for vectors allows us to write more expressive and readable code. By defining how operators should work with our custom objects, we can leverage familiar syntax and make our code more intuitive. Whether it is addition, subtraction, scalar multiplication, or equality comparison, operator overloading provides us with a powerful tool in vector operations.

#cpp #vector-math