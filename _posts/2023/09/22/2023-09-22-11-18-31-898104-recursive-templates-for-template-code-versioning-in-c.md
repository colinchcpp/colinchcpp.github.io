---
layout: post
title: "Recursive templates for template code versioning in C++"
description: " "
date: 2023-09-22
tags: [recursive, templates]
comments: true
share: true
---

In C++, templates are a powerful tool that allow code to be written in a way that is independent of data types. They provide a mechanism for code reusability and flexibility. However, when it comes to code versioning and managing different variations of a template, things can get complex.

One solution to this problem is to use recursive templates, which allow us to define a chain of templates that inherit from each other. Each template in the chain can introduce modifications or enhancements. Using this approach, we can create versioned template code that can be easily managed and maintained.

Let's consider an example where we have a template class called `Foo` that performs some computation on an input value. We want to version this template by adding different modifications to it, while still maintaining the original functionality.

```cpp
template <typename T>
class Foo {
public:
    Foo(const T& value) : m_value(value) {}

    T compute() {
        return m_value * 2; // Original computation
    }

protected:
    T m_value;
};

template <typename T>
class FooV1 : public Foo<T> {
public:
    using Foo<T>::Foo; // Inherit constructor

    T compute() {
        return Foo<T>::compute() + 10; // Computation with modification
    }
};

template <typename T>
class FooV2 : public Foo<T> {
public:
    using Foo<T>::Foo; // Inherit constructor

    T compute() {
        return Foo<T>::compute() - 5; // Computation with another modification
    }
};
```

In the above code, we have the `Foo` template class which represents the original version of our code. Then, we define `FooV1` and `FooV2` classes which inherit from `Foo` and modify the `compute()` function to add different variations.

Using these versioned templates, we can write code that chooses the appropriate version based on specific requirements or conditions.

```cpp
int main() {
    Foo<int> foo1(5);
    std::cout << foo1.compute() << std::endl; // Output: 10

    FooV1<int> foo2(5);
    std::cout << foo2.compute() << std::endl; // Output: 20

    FooV2<int> foo3(5);
    std::cout << foo3.compute() << std::endl; // Output: 5

    return 0;
}
```

In the `main()` function, we demonstrate using different versions of our `Foo` class. We create instances of `Foo`, `FooV1`, and `FooV2` and call the `compute()` function to see the output based on the versioned modifications.

By using recursive templates like this, we can easily manage and version our template code without duplicating a lot of boilerplate code. It provides a clean and concise way to handle different variations and modifications.

#recursive #templates