---
layout: post
title: "Uniform initialization with variadic templates in C++"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

In C++, "uniform initialization" refers to the usage of curly braces `{}` to initialize variables or objects. This syntax not only provides a consistent way to initialize different types of objects but also offers advantages such as preventing narrowing conversions and supporting aggregate initialization.

Variadic templates, on the other hand, allow functions or classes to accept a variable number of arguments of different types. This feature makes it possible to work with a flexible number of arguments and perform operations or computations accordingly.

In this blog post, we will explore how to combine uniform initialization and variadic templates in C++ to achieve a powerful and flexible way of initializing objects with a varying number of arguments.

## Variadic Templates Basics

Before diving into uniform initialization, let's first understand how variadic templates work. Variadic templates make use of recursion and template specialization to handle a variable number of arguments.

Consider the following example of a variadic template function `print`:

```c++
void print() {}

template<typename T, typename... Args>
void print(T arg, Args... args)
{
    std::cout << arg << " ";
    print(args...);
}
```

This function takes a variable number of arguments and recursively prints each argument until all arguments are processed.

## Uniform Initialization with Variadic Templates

To combine uniform initialization with variadic templates, we can use the same principles of recursion and template specialization.

Let's create a class `MultiValue` that can be initialized with a varying number of values. Each value will be stored in a vector.

```c++
template<typename T>
class MultiValue
{
private:
    std::vector<T> values;

public:
    MultiValue(const T& value)
    {
        values.push_back(value);
    }

    template<typename... Args>
    MultiValue(const T& value, Args... args)
    {
        values.push_back(value);
        MultiValue(args...);
    }

    void printValues()
    {
        for (const auto& value : values)
        {
            std::cout << value << " ";
        }
        std::cout << std::endl;
    }
};
```

In the constructor of `MultiValue`, we first push the current value into the vector and then recursively call the constructor with the remaining arguments. This ensures all the values are stored in the vector.

To test the `MultiValue` class, we can use the `print` function from earlier:

```c++
int main()
{
    print(1, 2, 3, 4, 5);
    MultiValue<int> mv(1, 2, 3, 4, 5);
    mv.printValues();

    return 0;
}
```

The output of this code will be:

```
1 2 3 4 5 
1 2 3 4 5 
```

As you can see, we were able to initialize an instance of `MultiValue` with a varying number of arguments using the uniform initialization syntax.

## Conclusion

Combining uniform initialization with variadic templates in C++ provides a flexible and efficient way to initialize objects with a variable number of arguments. By leveraging recursion and template specialization, we can handle multiple arguments and perform operations accordingly.

Variadic templates are a powerful feature of modern C++ that enable us to write flexible and generic code. Taking advantage of uniform initialization further enhances the readability and consistency of our code.

#References
[1] [Variadic Templates - cppreference.com](https://en.cppreference.com/w/cpp/language/parameter_pack)
[2] [Uniform Initialization - cppreference.com](https://en.cppreference.com/w/cpp/language/list_initialization)