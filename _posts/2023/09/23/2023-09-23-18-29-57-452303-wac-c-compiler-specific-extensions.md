---
layout: post
title: "WAC C++ Compiler-specific extensions"
description: " "
date: 2023-09-23
tags: [programming, WACCplusplusExtensions]
comments: true
share: true
---

When developing software using the WAC C++ compiler, developers have access to a number of compiler-specific extensions that can enhance their code performance and functionality. These extensions provide additional features and optimizations that are specific to the WAC compiler.

In this blog post, we will explore some of the notable WAC C++ compiler-specific extensions and how they can be utilized to improve your code.

## __attribute__((wac_noinline))

The `__attribute__((wac_noinline))` extension is used to prevent the compiler from inlining a particular function. Inlining is a compiler optimization technique where the compiler replaces a function call with the function's code directly inline, eliminating the overhead of function call overhead. However, in some cases, inlining certain functions may not be desirable, such as recursive functions or functions that need to be dynamically linked. By using the `__attribute__((wac_noinline))` extension, you can instruct the WAC compiler to not inline specific functions.

Example usage:

```cpp
__attribute__((wac_noinline))
void myFunction() {
  // Function code
}
```

## __attribute__((wac_pure))

The `__attribute__((wac_pure))` extension is used to declare a function as "pure," indicating that the function does not have any side effects and only depends on its input arguments. This allows the compiler to perform additional optimizations since it knows that the function's return value only depends on its input, making it suitable for constant folding and common subexpression elimination.

Example usage:

```cpp
__attribute__((wac_pure))
int square(int num) {
  return num * num;
}
```

## Conclusion

WAC C++ compiler-specific extensions provide developers with additional features and optimizations that can improve the performance and functionality of their code. The `__attribute__((wac_noinline))` extension allows developers to prevent function inlining when required, while the `__attribute__((wac_pure))` extension helps the compiler optimize functions that have no side effects.

By leveraging these extensions, developers can take full advantage of the WAC C++ compiler's capabilities and create more efficient and optimized code.

#programming #WACCplusplusExtensions