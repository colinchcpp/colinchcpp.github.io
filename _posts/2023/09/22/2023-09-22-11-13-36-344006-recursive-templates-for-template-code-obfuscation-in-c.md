---
layout: post
title: "Recursive templates for template code obfuscation in C++"
description: " "
date: 2023-09-22
tags: [cplusplus, templateprogramming]
comments: true
share: true
---

When it comes to writing clean and maintainable code, it's important to strive for readability and clarity. However, there may be cases where you want to obfuscate your code to hide its underlying logic. In this blog post, we will explore the use of recursive templates in C++ to achieve template code obfuscation.

## Understanding Recursive Templates

Recursive templates in C++ allow you to define a template that uses itself as a template argument. This recursive nature enables you to perform complex computations or operations at compile-time.

To illustrate this concept, let's create a simple example where we want to obfuscate a mathematical operation - adding two numbers. Here is the template code that achieves this using recursion:

```cpp
template<int N, int M>
struct Add {
    static const int value = Add<N - 1, M - 1>::value;
};

template<int M>
struct Add<0, M> {
    static const int value = M;
};
```

In this example, the `Add` template takes two integer arguments `N` and `M`. It recursively subtracts 1 from both `N` and `M` until `N` reaches 0. At that point, it returns the value of `M`, effectively adding `N` and `M` together.

## Template Code Obfuscation

To obfuscate the code further, you can make use of complex template meta-programming techniques. For example, you can add additional layers of recursion or use template specialization to implement more convoluted logic.

Here's an example of a more obfuscated version of the above code:

```cpp
template<int N, int M>
struct Add {
    static const int value = Add<N - 1, M - 1>::value * Add<N - 1, M - 1>::value;
};

template<int M>
struct Add<0, M> {
    static const int value = M + 42;
};
```

In this version, the result of the addition is multiplied by the recursively calculated value of `Add<N - 1, M - 1>`. Additionally, when `N` reaches 0, the result is further obfuscated by adding 42 to it.

## Conclusion

Recursive templates in C++ offer a powerful way to obfuscate your template code. By leveraging the recursion feature, combined with template meta-programming techniques, you can create highly convoluted and difficult-to-understand code.

It's worth noting that obfuscating code can make it harder to maintain and debug, and should only be used if there is a valid reason for doing so, such as protecting intellectual property or preventing reverse engineering.

Keep in mind that readability and maintainability should still be prioritized in most cases. Obfuscation should only be considered as a last resort and used sparingly.

#cplusplus #templateprogramming