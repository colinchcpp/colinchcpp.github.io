---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

When working with arrays or containers in C++, sorting the elements in a particular order is a common requirement. By default, C++ provides sorting algorithms that work well with most data types. However, there may be situations where you need to define custom sorting logic based on specific criteria or requirements. 

Fortunately, C++ allows you to define your own sorting literals that can be used with the standard sorting algorithms. This enables you to have more control over the order in which elements are sorted.

## Defining Custom Sorting Literals

To define a custom sorting literal, you need to define a comparison function or a functor that defines the sorting logic based on your specific criteria. The comparison function or functor should take two parameters and return a boolean value indicating the relative order of the elements.

Here's an example of a comparison function that sorts integers in descending order:

```cpp
bool descendingOrder(int a, int b) {
    return a > b;
}
```

You can also use lambda functions to define the comparison logic inline. Here's an example of using a lambda function to sort strings in ascending order of their lengths:

```cpp
std::sort(strings.begin(), strings.end(), [](const std::string& a, const std::string& b) {
    return a.length() < b.length();
});
```

## Using Custom Sorting Literals

Once you have defined your custom sorting literal, you can use it with the standard sorting algorithms like `std::sort`, `std::stable_sort`, or `std::partial_sort`. Simply pass the custom sorting literal as the third argument when calling the sorting function.

Using the previously defined comparison function for descending order, you can sort an array of integers as follows:

```cpp
std::sort(array.begin(), array.end(), descendingOrder);
```

Similarly, if you have a vector of strings and want to sort them based on their lengths in ascending order, you can use the lambda function as follows:

```cpp
std::sort(strings.begin(), strings.end(), [](const std::string& a, const std::string& b) {
    return a.length() < b.length();
});
```

## Conclusion

Using custom sorting literals in C++ allows you to have more control over the sorting order of your elements. Whether you need to sort based on a specific criteria or define a completely custom sorting logic, this feature provides flexibility and customization options.

By defining your own comparison functions or functors, you can tailor the sorting process to fit your unique requirements. Experiment with different sorting literals to achieve the desired order for your data.

#References
- [C++ Reference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Reference - Lambda Expressions](https://en.cppreference.com/w/cpp/language/lambda)