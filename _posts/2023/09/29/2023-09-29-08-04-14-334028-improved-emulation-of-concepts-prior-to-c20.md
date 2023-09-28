---
layout: post
title: "Improved emulation of concepts prior to C++20"
description: " "
date: 2023-09-29
tags: [EmulatingConcepts]
comments: true
share: true
---

In the world of modern programming, C++ stands as a powerful and efficient programming language. However, prior to the release of C++20, concepts were not officially supported within the language. Concepts are a vital tool to define constraints on templates, making code more readable and expressive. But fear not, there are ways to emulate concepts in earlier versions of C++! In this article, we will explore some techniques to achieve this emulation.

## Interface-based Emulation

One way to emulate concepts before C++20 is through **interface-based emulation**. This technique involves creating base classes that represent the desired concepts and having template functions or classes inherit from these base classes. This way, we can enforce constraints on the template arguments by using the base class as a type constraint. Although this approach can add some extra lines of code, it provides a way to achieve concept-like behavior.

```cpp
class Printable {
public:
    virtual void print() const = 0;
};

template <typename T>
struct MyContainer : public Printable {
    // ...
    void print() const override {
        for (const auto& element : container) {
            std::cout << element << " ";
        }
        std::cout << std::endl;
    }
    // ...
};
```

Here, we create an interface class `Printable` with a pure virtual function `print()`. Then, the `MyContainer` template struct inherits from `Printable`, enforcing that any type `T` used as a template argument must implement the `print()` function.

## SFINAE-based Emulation

Another approach to emulate concepts prior to C++20 is through the usage of **SFINAE** (Substitution Failure is Not An Error) technique. This technique relies on enabling or disabling function or template overloads based on the substitution failure of certain expressions. By adding a series of `std::enable_if` conditions, we can constrain the template arguments to meet our desired concepts.

```cpp
template <typename T>
typename std::enable_if_t<std::is_integral_v<T>>
print_num(const T& num) {
    std::cout << "Integer: " << num << std::endl;
}

template <typename T>
typename std::enable_if_t<std::is_floating_point_v<T>>
print_num(const T& num) {
    std::cout << "Floating point: " << num << std::endl;
}
```

In the code above, we have two overload functions `print_num`. The first overload will only be enabled if `T` is an integral type, and the second overload will only be enabled if `T` is a floating-point type. Thus, we can enforce constraints on the template argument `T` using `std::enable_if` with the help of SFINAE.

## #EmulatingConcepts #C++Programming

Emulating concepts prior to C++20 allows us to write cleaner and more expressive code, even before the official introduction of concepts in the language. By using interface-based emulation or SFINAE-based emulation techniques, we can define constraints on templates and improve code readability. As we wait to fully embrace C++20 and its native concepts, these emulation techniques provide a practical solution for modern programming in earlier versions of C++.