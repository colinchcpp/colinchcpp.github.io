---
layout: post
title: "How to overload arithmetic operators in C++"
description: " "
date: 2023-09-14
tags: [OperatorOverloading]
comments: true
share: true
---

In C++, you can overload arithmetic operators to work with custom types. This allows you to define how the operators behave when used with objects of your own classes.

## Operator Overloading Syntax

To overload arithmetic operators in C++, you need to define a member function or a non-member function that implements the desired behavior for the operator. The general syntax for overloading an arithmetic operator is as follows:

```cpp
return_type operator<operator_symbol>(const <class_name>& operand);
```

For example, to overload the addition operator (`+`) for a class called `MyClass`, you would define it as follows:

```cpp
return_type operator+(const MyClass& operand);
```

## Example: Overloading the Addition Operator

Let's consider a `Vector` class that represents a mathematical vector with `x` and `y` coordinates. We can overload the `+` operator to implement vector addition.

```cpp
class Vector {
private:
  double x;
  double y;
  
public:
  Vector(double xCoord, double yCoord) : x(xCoord), y(yCoord) {}

  Vector operator+(const Vector& other) {
    double newX = this->x + other.x;
    double newY = this->y + other.y;
    return Vector(newX, newY);
  }
};
```

In this example, we define the `+` operator as a member function of the `Vector` class. It takes a `Vector` object as its parameter and returns a new `Vector` object that represents the sum of the two vectors.

## Usage

We can now use the overloaded addition operator to add two `Vector` objects:

```cpp
Vector v1(1.0, 2.0);
Vector v2(3.0, 4.0);

Vector v3 = v1 + v2;  // Overloaded addition operator

// Output the result
std::cout << "v3 = (" << v3.getX() << ", " << v3.getY() << ")" << std::endl;
```

The output will be:

```
v3 = (4, 6)
```

## Conclusion

Operator overloading in C++ allows you to extend the functionality of arithmetic operators to work with custom types. This can make your code more expressive and intuitive. Remember to use operator overloading judiciously, and make sure your overloaded operators adhere to the expected behavior.

#C++ #OperatorOverloading