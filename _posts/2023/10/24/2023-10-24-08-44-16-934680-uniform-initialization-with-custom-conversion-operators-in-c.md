---
layout: post
title: "Uniform initialization with custom conversion operators in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In C++, uniform initialization allows us to initialize objects using curly braces (`{}`). It provides a more consistent and readable way to initialize objects, and it can be used in a variety of contexts, such as initializing variables, passing arguments to functions, and initializing container classes.

However, when using uniform initialization, we may encounter situations where the compiler cannot determine the correct conversion between the types involved. In such cases, we can make use of custom conversion operators to provide explicit conversion rules.

## Custom Conversion Operators

Custom conversion operators in C++ allow us to define our own conversion rules between types. They are member functions of a class or struct and are used to convert objects of one type to another.

To define a conversion operator, we use the `operator` keyword followed by the target type we want to convert to. Let's consider an example where we want to convert an `int` to a `CustomType`:

```cpp
struct CustomType {
    int value;

    explicit operator int() const {
        return value;
    }
};
```

In the above code, we define a conversion operator that converts a `CustomType` object to an `int`. The `explicit` keyword makes the conversion explicit, meaning it won't happen implicitly.

## Uniform Initialization with Custom Conversion

With custom conversion operators, we can now use uniform initialization to initialize objects of our custom type. Let's see an example:

```cpp
CustomType obj = {42};
```

In the above code, we initialize a `CustomType` object `obj` using uniform initialization with the value `42`. Since we have defined a conversion operator from `int` to `CustomType`, the compiler will use that conversion to create the `CustomType` object.

## Conclusion

Uniform initialization in C++ provides a concise and consistent way to initialize objects. However, in cases where the compiler cannot determine the correct conversion between types, we can utilize custom conversion operators to provide explicit conversion rules.

By defining custom conversion operators, we can use uniform initialization with our custom types and ensure the correct conversions take place.

**References:**

- [Uniform Initialization - cppreference](https://en.cppreference.com/w/cpp/language/list_initialization)
- [Conversion Operators - cppreference](https://en.cppreference.com/w/cpp/language/cast_operator)