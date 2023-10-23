---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a common operation used in programming to arrange elements in a specific order. By default, most programming languages provide built-in sorting mechanisms for basic data types like integers and strings. However, there are cases where we may need to sort custom objects or use a specific sorting order for certain literals. In this article, we will explore how to achieve custom sorting literals in C++.

## Table of Contents
- [Introduction](#introduction)
- [The `std::sort()` Function](#the-stdsort-function)
- [Custom Sorting Functors](#custom-sorting-functors)
- [Lambda Expressions](#lambda-expressions)
- [Conclusion](#conclusion)

## Introduction

In C++, you can customize the sorting behavior by providing your own comparison function or functor. The comparison function defines the order in which the elements should be sorted.

## The `std::sort()` Function

The `std::sort()` function in the C++ Standard Library is commonly used for sorting containers like vectors, arrays, and lists. By default, it uses the less-than (`<`) operator for comparison.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> numbers = {3, 1, 4, 1, 5, 9, 2, 6};

    std::sort(numbers.begin(), numbers.end());

    for (const auto& number : numbers) {
        std::cout << number << " ";
    }

    return 0;
}
```

Output:
```
1 1 2 3 4 5 6 9
```

In the example above, we use `std::sort()` to sort a vector of integers in ascending order.

## Custom Sorting Functors

To achieve custom sorting literals, we can define our own functors to use as the comparison function. A functor is an object that can be invoked like a function.

```cpp
#include <algorithm>
#include <iostream>

struct LengthComparator {
    bool operator()(const std::string& str1, const std::string& str2) const {
        return str1.length() < str2.length();
    }
};

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};

    std::sort(words.begin(), words.end(), LengthComparator());

    for (const auto& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

Output:
```
date apple cherry banana
```

In this example, we define a custom functor called `LengthComparator` that compares two strings based on their lengths. We pass an instance of the `LengthComparator` functor as the comparison function to `std::sort()`.

## Lambda Expressions

Since C++11, lambda expressions allow us to define anonymous functions inline. We can use lambda expressions to provide custom sorting behavior without explicitly defining a separate functor.

```cpp
#include <algorithm>
#include <iostream>

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};

    std::sort(words.begin(), words.end(), [](const std::string& str1, const std::string& str2) {
        return str1.length() < str2.length();
    });

    for (const auto& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

Output:
```
date apple cherry banana
```

In this example, we use a lambda expression as the comparison function for `std::sort()`. The lambda expression compares two strings based on their lengths.

## Conclusion

In C++, custom sorting literals can be achieved by providing a custom comparison function or functor to the `std::sort()` function. This allows us to sort elements according to our specific requirements, beyond the default sorting behavior. Whether using custom functors or lambda expressions, C++ provides powerful options for fine-tuning the sorting order.