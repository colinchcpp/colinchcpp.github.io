---
layout: post
title: "Overloading bitwise shift operators in C++"
description: " "
date: 2023-09-14
tags: [BitwiseOperators]
comments: true
share: true
---

In C++, you can overload the bitwise shift operators (`<<` and `>>`) to provide custom behavior for your classes. This allows you to use these operators with your own data types, giving you more flexibility and control.

## Overloading the Left Shift `<<` Operator ##

To overload the left shift operator (`<<`), you need to define a member function or a friend function that takes two parameters: the left operand (`ostream&`, in most cases) and the right operand (your custom type).

Here's an example of overloading the `<<` operator for a custom class called `MyClass`:

```cpp
class MyClass {
public:
    // ... other class members

    // Overloading the left shift operator
    friend std::ostream& operator<<(std::ostream& os, const MyClass& obj) {
        // Custom logic to output MyClass object to the stream
        os << "Custom output: " << obj.someMember;
        return os;
    }
};
```

With this overload, you can now use the `<<` operator to print objects of your `MyClass` type in a customized way:

```cpp
MyClass obj;
std::cout << obj << std::endl; // Output: Custom output: <someMember value>
```

## Overloading the Right Shift `>>` Operator ##

To overload the right shift operator (`>>`), you need to define a member function or a friend function that takes two parameters: the left operand (`istream&`, in most cases) and the right operand (your custom type).

Here's an example of overloading the `>>` operator for the same `MyClass`:

```cpp
class MyClass {
public:
    // ... other class members

    // Overloading the right shift operator
    friend std::istream& operator>>(std::istream& is, MyClass& obj) {
        // Custom logic to input data from the stream into MyClass object
        is >> obj.someMember;
        return is;
    }
};
```

With this overload, you can now use the `>>` operator to input values into objects of your `MyClass` type:

```cpp
MyClass obj;
std::cin >> obj; // User input will be assigned to obj.someMember
```

## Conclusion ##

Overloading the bitwise shift operators in C++ allows you to define custom behavior when using these operators with your own classes. This can be useful for outputting objects in a specialized format or inputting values into objects in a specific way. By using operator overloading, you can make your code more expressive and intuitive.

#C++ #BitwiseOperators