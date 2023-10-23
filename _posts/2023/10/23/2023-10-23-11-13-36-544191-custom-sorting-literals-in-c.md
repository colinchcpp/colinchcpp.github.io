---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In many programming tasks, we often encounter situations where we need to sort a collection of elements based on specific criteria. The standard C++ library provides us with the `std::sort` function to sort elements using default comparison operators. However, there are cases where we might want to define our own custom sorting order.

In this blog post, we will explore how to implement custom sorting literals in C++. By using custom comparison functions or function objects, we can define our own rules for sorting elements within a collection.

## Using Custom Comparison Function

One way to implement custom sorting literals is by using a custom comparison function. This function should take two elements as input parameters and return `true` if the first element should come before the second element in the sorted order, or `false` otherwise.

Let's say we have a collection of strings and we want to sort them based on their length. We can define a custom comparison function that compares the lengths of two strings:

```cpp
bool compareLength(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}
```

We can then pass this custom comparison function as the third argument to the `std::sort` function, along with the begin and end iterators of our collection:

```cpp
std::vector<std::string> strings = { "apple", "banana", "cherry", "date" };
std::sort(strings.begin(), strings.end(), compareLength);
```

After sorting, the `strings` vector will contain the elements in the following order: `date`, `apple`, `cherry`, `banana`. The elements are sorted based on their length.

## Using Custom Comparison Function Object

Alternatively, we can use a custom comparison function object instead of a function. A function object is a class that overloads the `operator()` to define the comparison behavior. This allows us to create objects that behave as functions.

Let's rewrite our previous example using a custom comparison function object:

```cpp
struct CompareLength {
    bool operator()(const std::string& str1, const std::string& str2) const {
        return str1.length() < str2.length();
    }
};
```

We can then create an instance of this class and pass it as the third argument to `std::sort`:

```cpp
std::vector<std::string> strings = { "apple", "banana", "cherry", "date" };
std::sort(strings.begin(), strings.end(), CompareLength());
```

The result will be the same as before, with the `strings` vector sorted based on the length of the elements.

## Conclusion

Custom sorting literals allow us to define our own rules for sorting elements in C++. By using custom comparison functions or function objects, we can sort elements based on any criteria we desire.

In this blog post, we explored how to use custom comparison functions and function objects to implement custom sorting literals in C++. This gives us the flexibility to sort elements based on any custom logic we need.

#References
- [`std::sort` - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)