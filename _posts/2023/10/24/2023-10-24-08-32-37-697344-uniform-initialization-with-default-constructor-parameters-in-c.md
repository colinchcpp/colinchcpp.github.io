---
layout: post
title: "Uniform initialization with default constructor parameters in C++"
description: " "
date: 2023-10-24
tags: [default]
comments: true
share: true
---

In C++, we often use constructors to initialize objects. Prior to C++11, it was common to use different constructors with different parameter lists to provide default values for object initialization. However, with the introduction of uniform initialization syntax, we can now achieve the same result using default constructor parameters.

## Default constructor parameters

Default constructor parameters allow us to provide default values for function parameters in the constructor declaration. They specify values that are used when no arguments are passed during object initialization.

Consider the following example:

```cpp
class Rectangle {
  int width;
  int height;
public:
  Rectangle(int w = 0, int h = 0) : width(w), height(h) { }
};
```

In the above code, the `Rectangle` class has a constructor with default parameters `int w = 0` and `int h = 0`. These default values will be used if no arguments are provided during object initialization.

## Uniform initialization with default constructor parameters

With uniform initialization, we can initialize objects using braces `{}`. We can also omit the constructor arguments, allowing the default constructor parameters to take effect.

Here's an example:

```cpp
Rectangle r1;             // width = 0, height = 0
Rectangle r2{};           // width = 0, height = 0
Rectangle r3{10};         // width = 10, height = 0
Rectangle r4{10, 20};     // width = 10, height = 20
```

In the above code, we have created four instances of the `Rectangle` class using uniform initialization. In `r1` and `r2`, no arguments are provided, so the default constructor parameters `0` will be used for both `width` and `height`. In `r3`, only the `width` is provided, so `0` is used for `height`. Finally, `r4` has both `width` and `height` explicitly specified.

## Benefits of using default constructor parameters

Using default constructor parameters with uniform initialization provides several benefits:

1. **Simpler syntax**: The code becomes more concise and easier to read without the need for multiple constructors with different parameter lists.
2. **Flexibility**: Default constructor parameters allow for object initialization using both explicit and implicit values.
3. **Backward compatibility**: The use of default constructor parameters does not affect existing code and is fully compatible with older C++ syntax.

## Conclusion

Default constructor parameters in combination with uniform initialization provide a streamlined and flexible way to initialize objects in C++. They simplify code and allow for more concise and readable constructors. By adopting these features, developers can benefit from improved code readability and maintainability in their C++ projects.

---

References:
- [C++ Default Arguments](https://www.cplusplus.com/doc/tutorial/functions2/#default_arguments)
- [Initializer List in C++](https://www.geeksforgeeks.org/initializer-list-cpp/)