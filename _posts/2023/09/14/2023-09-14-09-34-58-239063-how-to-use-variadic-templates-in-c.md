---
layout: post
title: "How to use variadic templates in C++?"
description: " "
date: 2023-09-14
tags: [include, VariadicTemplates]
comments: true
share: true
---

Variadic templates in C++ allow us to define functions or classes that can accept a variable number of arguments of different types. This powerful feature makes it possible to write more flexible and generic code. In this blog post, we'll explore how to use variadic templates in C++.

## Syntax

The syntax for defining a variadic template is as follows:

```cpp
template <typename... Args>
ReturnType functionName(Args... args) {
  // Function body
}
```

The ellipsis `...` represents the variadic part, and the pack `Args` is a template parameter pack that can hold zero or more types.

## Example: Printing Multiple Arguments

Let's start with a simple example of a function that prints multiple arguments to the console:

```cpp
#include <iostream>

// Base case for recursion - prints the last argument
void printArguments() {}

// Variadic template function to print multiple arguments
template <typename T, typename... Args>
void printArguments(T first, Args... rest) {
  std::cout << first << " ";
  printArguments(rest...);
}

int main() {
  printArguments("Hello", "World", 10, 3.14);
  return 0;
}
```

In this example, the `printArguments` function takes the first argument and prints it to the console. Then, it recursively calls itself with the remaining arguments, until no arguments are left.

## Use Case: Generic Sum Function

Variadic templates are particularly useful when dealing with operations that need to be performed on a variable number of arguments. Let's look at an example of a generic sum function:

```cpp
#include <iostream>

// Base case for recursion - returns 0
template <typename T>
T sum(T arg) {
  return arg;
}

// Variadic template function to calculate the sum of arguments
template <typename T, typename... Args>
T sum(T first, Args... rest) {
  return first + sum(rest...);
}

int main() {
  std::cout << sum(1, 2, 3, 4, 5) << std::endl;
  return 0;
}
```

In this example, the `sum` function recursively adds the first argument to the sum of the remaining arguments, until no arguments are left. This allows us to calculate the sum of any number of arguments, regardless of their types.

## Conclusion

Variadic templates in C++ provide a powerful tool for writing generic and flexible code that can handle a variable number of arguments. The ability to work with packs of types opens up new possibilities for designing reusable and versatile functions and classes. By leveraging variadic templates, you can enhance the flexibility and expressiveness of your C++ code.

*#C++ #VariadicTemplates*