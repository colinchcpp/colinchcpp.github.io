---
layout: post
title: "Conditional initialization using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [uniform, programming]
comments: true
share: true
---

In modern C++, uniform initialization syntax (also known as brace initialization) is a powerful feature that allows us to initialize objects in a consistent manner. It provides a concise and readable way of initializing variables, arrays, and class objects.

One of the notable advantages of uniform initialization is its ability to perform conditional initialization, where the initialization value is determined based on a condition. This can be done using the ternary operator within the brace initializer.

Let's take a look at an example to illustrate conditional initialization using uniform initialization in C++:

```cpp
#include <iostream>

int main() {
    bool isEven = true;

    int number = isEven ? 2 : 1;
    std::cout << "The number is: " << number << std::endl;

    return 0;
}
```

In the above code, we have a boolean variable `isEven` that determines whether the number should be even or odd. We use the ternary operator `? :` within the brace initializer to conditionally initialize the `number` variable.

If `isEven` is `true`, the value `2` is assigned to `number`. Otherwise, if `isEven` is `false`, the value `1` is assigned. Finally, we output the value of `number` to the console.

The output of this code will be:
```
The number is: 2
```

By using uniform initialization with the ternary operator, we can simplify the conditional initialization process and write more expressive code.

Uniform initialization is not limited to simple types like integers. It can also be used with user-defined classes and containers such as arrays or std::vector. The flexibility and readability provided by uniform initialization make it a valuable tool in modern C++ programming.

To learn more about uniform initialization in C++, you can refer to the following resources:

- [C++ Reference: Uniform initialization](https://en.cppreference.com/w/cpp/language/list_initialization)
- [Bjarne Stroustrup's C++11 FAQ](http://www.stroustrup.com/C++11FAQ.html#uniform-init)
- [Effective Modern C++: Item 7 - Distinguish between () and {} when creating objects](https://www.amazon.com/Effective-Modern-Specific-Ways-Improve/dp/1491903996/)

#cpp #programming