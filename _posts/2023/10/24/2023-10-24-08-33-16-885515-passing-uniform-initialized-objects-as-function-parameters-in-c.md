---
layout: post
title: "Passing uniform initialized objects as function parameters in C++"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with C++, you may come across situations where you need to pass objects as parameters to functions. In C++11 and later versions, you can use uniform initialization to create objects in a more concise and readable way. In this blog post, we will explore how to pass uniform initialized objects as function parameters in C++.

## Table of Contents
- [What is uniform initialization?](#what-is-uniform-initialization)
- [Passing uniform initialized objects as function parameters](#passing-uniform-initialized-objects-as-function-parameters)
- [Example code](#example-code)
- [Conclusion](#conclusion)
- [References](#references)

## What is uniform initialization?

Uniform initialization in C++ allows you to initialize objects in a consistent and uniform manner using curly braces `{}`. This feature was introduced in C++11 to provide a more concise and intuitive syntax for initializing objects.

Before uniform initialization:

```cpp
int x = 10;
std::string name = "John";
std::vector<int> numbers = {1, 2, 3};
```

With uniform initialization:

```cpp
int x{10};
std::string name{"John"};
std::vector<int> numbers{1, 2, 3};
```

Uniform initialization is not limited to built-in types. You can also use it to initialize user-defined types, such as custom classes and structures.

## Passing uniform initialized objects as function parameters

When passing uniform initialized objects as function parameters, you can simply pass the object using the same curly braces syntax.

```cpp
void printVector(const std::vector<int>& vec) {
    for (const auto& item : vec) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
}

int main() {
    printVector({1, 2, 3, 4, 5});
    return 0;
}
```

In the example above, we define a function `printVector` that takes a `const std::vector<int>&` parameter. We can pass a uniform initialized vector directly as an argument when calling the function.

## Example code

Here's an example that demonstrates passing uniform initialized objects as function parameters:

```cpp
#include <iostream>
#include <vector>

void printVector(const std::vector<int>& vec) {
    for (const auto& item : vec) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
}

int main() {
    printVector({1, 2, 3, 4, 5});
    return 0;
}
```

Output:

```
1 2 3 4 5
```

## Conclusion

Passing uniform initialized objects as function parameters in C++ is a convenient way to create and pass objects in a concise and readable manner. It improves code readability and eliminates the need for temporary variables. By using uniform initialization, you can follow a consistent syntax and express your intentions clearly.

## References

- [C++ Reference: Uniform initialization](https://en.cppreference.com/w/cpp/language/list_initialization)