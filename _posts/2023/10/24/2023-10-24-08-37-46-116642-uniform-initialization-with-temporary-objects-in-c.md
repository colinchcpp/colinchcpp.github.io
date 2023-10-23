---
layout: post
title: "Uniform initialization with temporary objects in C++"
description: " "
date: 2023-10-24
tags: [tech]
comments: true
share: true
---

In C++, you can initialize objects using uniform initialization syntax, which was introduced in C++11. Uniform initialization allows you to initialize an object with a set of values enclosed in curly braces `{}`. It provides a more consistent and concise way of initializing objects compared to traditional constructor syntax.

One interesting use case of uniform initialization is with temporary objects. A temporary object is a short-lived object that is created and destroyed within a single expression. Prior to C++11, initializing temporary objects involved invoking the constructor explicitly. However, with uniform initialization, you can initialize temporary objects directly using the same syntax as regular objects.

Here's an example to showcase uniform initialization with temporary objects:

```cpp
#include <iostream>

class Point {
public:
    int x, y;

    Point(int x, int y) : x(x), y(y) {
        std::cout << "Constructor called" << std::endl;
    }
};

int main() {
    Point p = {3, 4}; // Initialize temporary object directly

    std::cout << "p.x: " << p.x << ", p.y: " << p.y << std::endl;

    return 0;
}
```

In the above example, we have a `Point` class that takes `x` and `y` coordinates in its constructor. We initialize a temporary object of `Point` class directly using uniform initialization syntax `{3, 4}`. The temporary object is then used to initialize the `p` object of `Point` class.

When the program runs, the constructor of the `Point` class is called for both the temporary object and the `p` object. The output will be:

```plaintext
Constructor called
Constructor called
p.x: 3, p.y: 4
```

As you can see, the constructor is invoked once for the temporary object and once for the `p` object.

Uniform initialization with temporary objects is quite useful when working with standard library containers or passing arguments to a function by value. It allows for a cleaner and more consistent way of initializing objects without the need for separate constructor calls or explicit conversion.

So, whenever you need to initialize a temporary object in C++, consider using uniform initialization syntax to improve code readability and maintainability.

**References:**

- [Uniform Initialization - cppreference.com](https://en.cppreference.com/w/cpp/language/initialization)
- [C++11 Uniform Initialization](https://www.geeksforgeeks.org/uniform-initialization-in-c/)

#tech #cpp