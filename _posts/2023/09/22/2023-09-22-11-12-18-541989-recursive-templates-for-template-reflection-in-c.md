---
layout: post
title: "Recursive templates for template reflection in C++"
description: " "
date: 2023-09-22
tags: [templates, reflection]
comments: true
share: true
---

Template metaprogramming is a powerful technique in C++ that allows compile-time computation and introspection. One interesting application of template metaprogramming is template reflection, where we can statically inspect the properties of a template.

In this blog post, we will explore how to implement recursive templates for template reflection in C++. We will leverage the power of variadic templates and constexpr to achieve this.

## What is Template Reflection?

Template reflection refers to the ability to analyze and query properties of a template at compile-time. With template reflection, we can programmatically inspect template parameters, extract information about them, and perform operations based on that information.

## Recursive Templates for Template Reflection

Let's consider a simple example where we want to reflect on a given template `MyTemplate`:

```cpp
template <typename T, int N>
struct MyTemplate {
    // ... implementation ...
};
```

We can start by defining a primary template called `Reflect`. This template will form the basis of our recursive reflection process:

```cpp
template <typename T>
struct Reflect {
    // Base case: when T is not a specialization of MyTemplate
    constexpr static bool is_template_instance = false;
    constexpr static int num_parameters = 0;
};

```

Next, we can specialize the `Reflect` template for the `MyTemplate` class:

```cpp
template <typename T, int N>
struct Reflect<MyTemplate<T, N>> {
    constexpr static bool is_template_instance = true;
    constexpr static int num_parameters = 2;
};
```

Now, we can define a helper function called `reflect` that will use recursive partial template specialization to iterate over each template parameter:

```cpp
template <typename T>
constexpr void reflect() {
    // Base case: when T is not a specialization of MyTemplate
    if (!Reflect<T>::is_template_instance) {
        std::cout << "Not a template instance" << std::endl;
        return;
    }

    // Recursive case: when T is a specialization of MyTemplate
    std::cout << "Template instance with " << Reflect<T>::num_parameters << " parameters" << std::endl;

    // Reflect on each parameter
    reflect<typename T::template parameter<0>>();
    reflect<typename T::template parameter<1>>();
}
```

Finally, we can use our `reflect` function to inspect the template parameters of `MyTemplate`:

```cpp
int main() {
    reflect<MyTemplate<int, 5>>();
    return 0;
}
```

## Conclusion

Recursive templates for template reflection provide a powerful tool for analyzing and querying template parameters at compile-time. By leveraging the power of variadic templates and constexpr, we can explore the capabilities of template metaprogramming in C++. Stay curious and keep exploring the world of template metaprogramming!

#cpp #templates #reflection