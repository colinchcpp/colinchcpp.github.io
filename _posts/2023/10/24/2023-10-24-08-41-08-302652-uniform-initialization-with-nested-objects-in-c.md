---
layout: post
title: "Uniform initialization with nested objects in C++"
description: " "
date: 2023-10-24
tags: [es97]
comments: true
share: true
---

Uniform initialization is a powerful feature introduced in C++11 that allows us to initialize objects in a concise and consistent manner. One of the great advantages of uniform initialization is its ability to initialize nested objects easily and intuitively.

Consider the following scenario where we have a class `Address` that represents a mailing address, and a class `Person` that has an `Address` as one of its member variables:

```cpp
class Address {
public:
    Address(const std::string& street, const std::string& city, const std::string& country)
        : street(street), city(city), country(country) {}

private:
    std::string street;
    std::string city;
    std::string country;
};

class Person {
public:
    Person(const std::string& name, const Address& address)
        : name(name), address(address) {}

private:
    std::string name;
    Address address;
};
```

Traditionally, initializing the `Person` object with an `Address` object would require multiple lines of code. However, with uniform initialization, we can assign values to nested objects in a more compact and readable way.

```cpp
Person john{
    "John Doe",
    {"123 Main St", "New York", "USA"}
};
```

In the above code snippet, we create a `Person` object named "john" and provide values for its `name` and `address` members. The nested `Address` object is initialized using the same uniform initialization syntax, making the code more concise and self-explanatory.

Uniform initialization with nested objects becomes particularly useful when dealing with more complex data structures that involve multiple levels of nesting or containers.

Uniform initialization also works seamlessly with constructors that have default arguments. If the nested object's constructor has default arguments defined, you can omit those arguments during initialization, and the default values will be used.

```cpp
class Point {
public:
    Point(int x = 0, int y = 0) : x(x), y(y) {}

private:
    int x;
    int y;
};

class Rectangle {
public:
    Rectangle(const Point& topLeft, const Point& bottomRight)
        : topLeft(topLeft), bottomRight(bottomRight) {}

private:
    Point topLeft;
    Point bottomRight;
};

Rectangle rect{
    {0, 0}, // topLeft
    {10, 10} // bottomRight
};
```

In conclusion, uniform initialization in C++ provides a concise and consistent way to initialize objects, even when they are nested. It simplifies the code and improves readability, making it easier to understand the structure and initialization of complex data structures.

# References
- [C++ Documentation: Uniform Initialization](https://en.cppreference.com/w/cpp/language/initializer_list)
- [C++ Core Guidelines: Initialization](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es97-use-uniform-initialization-to-initialize-everything)