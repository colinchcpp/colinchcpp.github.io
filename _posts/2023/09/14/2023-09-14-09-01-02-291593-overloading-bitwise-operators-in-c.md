---
layout: post
title: "Overloading bitwise operators in C++"
description: " "
date: 2023-09-14
tags: [include, BitwiseOperators]
comments: true
share: true
---

Bitwise operators are an important part of C++ programming as they allow manipulation of individual bits within a variable. While C++ provides several bitwise operators such as `&`, `|`, `^`, `~`, `>>`, and `<<`, it is also possible to overload these operators to work with user-defined objects or custom data types. In this blog post, we will explore how to overload bitwise operators in C++.

## Operator Overloading Basics ##

Operator overloading enables us to redefine the behavior of an operator when used with user-defined objects. By overloading operators, we can make them work in a way that is meaningful for our custom types. The syntax for overloading bitwise operators is similar to other operator overloads in C++.

## Overloading Bitwise AND (`&`) Operator ##

To overload the bitwise AND operator (`&`), we need to define a function inside our class with the signature `operator&`. Here is an example:

```cpp
#include <iostream>

class BitwiseNumber
{
private:
    int value;
    
public:
    BitwiseNumber(int val)
    {
        value = val;
    }
    
    BitwiseNumber operator&(const BitwiseNumber& other) const
    {
        int result = value & other.value;
        return BitwiseNumber(result);
    }
    
    void printValue() const
    {
        std::cout << value << std::endl;
    }
};

int main()
{
    BitwiseNumber num1(5);
    BitwiseNumber num2(3);
    
    BitwiseNumber result = num1 & num2;
    result.printValue();
    
    return 0;
}
```

In the above code, we have defined a class `BitwiseNumber` with an overloaded `operator&` function. This function performs bitwise AND operation on the `value` member of both operands and returns a new `BitwiseNumber` object.

## Overloading Bitwise OR (`|`) Operator ##

Similarly, we can overload the bitwise OR operator (`|`) by defining a function named `operator|` inside our class. Here's an example:

```cpp
// Rest of the code

BitwiseNumber operator|(const BitwiseNumber& other) const
{
    int result = value | other.value;
    return BitwiseNumber(result);
}

// Rest of the code
```

In the above example, the overloaded `operator|` function computes the bitwise OR operation on the `value` member of two `BitwiseNumber` objects and returns a new object with the result.

## Conclusion ##

By overloading bitwise operators in C++, we can extend their functionality to work with custom types or user-defined objects. This gives us the flexibility to work with bitwise operations in a way that is meaningful for our specific use cases. Understanding operator overloading enables us to write more expressive and intuitive code.

Make sure to consult the C++ documentation for the complete list of allowed operator overloads and their signatures. Happy coding!

**#C++ #BitwiseOperators**