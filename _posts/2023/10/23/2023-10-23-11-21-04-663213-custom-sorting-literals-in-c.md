---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a fundamental operation in computer science and is frequently used in programming. When it comes to sorting, most programming languages provide default sorting mechanisms for common data types like integers, floating-point numbers, and strings. However, there may be scenarios where you need to sort data using custom ordering rules or criteria.

In C++, you can achieve custom sorting by utilizing a lambda function or a functor. This allows you to define your own comparison logic and sort data according to your specific requirements.

## Lambda Functions

Lambda functions are anonymous functions that can be defined inline within a program. They provide a concise way to define custom sorting rules without the need for writing separate comparison functions. Here's an example of using a lambda function to sort an array of integers in descending order:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
  std::vector<int> numbers = {5, 2, 8, 4, 1};
  
  std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
    return a > b;
  });
  
  for (const auto& number : numbers) {
    std::cout << number << " ";
  }
  
  return 0;
}
```

Output: `8 5 4 2 1`

In the above example, the `std::sort` function is used to sort the `numbers` vector. The lambda function `[](int a, int b) { return a > b; }` defines the custom sorting criteria where `a` is considered greater than `b`. This lambda function is passed as the third argument to the `std::sort` function.

## Functors

Functors, also known as function objects, are objects that can be treated as functions. They provide a more flexible way of defining custom sorting rules as compared to lambda functions, especially when complex comparison logic is involved.

Here's an example of using a functor to sort a vector of strings in lexicographic order, ignoring case sensitivity:

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <vector>

struct CaseInsensitiveComparator {
  bool operator()(const std::string& a, const std::string& b) const {
    // Convert strings to lowercase before comparison
    std::string lowerA = a;
    std::string lowerB = b;
    std::transform(lowerA.begin(), lowerA.end(), lowerA.begin(), ::tolower);
    std::transform(lowerB.begin(), lowerB.end(), lowerB.begin(), ::tolower);
    
    return lowerA < lowerB;
  }
};

int main() {
  std::vector<std::string> names = {"Alice", "bob", "Charlie", "danny"};
  
  std::sort(names.begin(), names.end(), CaseInsensitiveComparator());
  
  for (const auto& name : names) {
    std::cout << name << " ";
  }
  
  return 0;
}
```

Output: `Alice bob Charlie danny`

In the above example, a functor named `CaseInsensitiveComparator` is defined with an overloaded `()` operator. This operator compares two strings in a case-insensitive manner by converting them to lowercase before comparison. The `std::sort` function uses an instance of this functor as the third argument to perform the custom sorting.

## Conclusion

Custom sorting is a powerful feature of C++ that allows you to sort data according to your specific ordering criteria. By using lambda functions or functors, you can define custom comparison logic for sorting integers, strings, or any other data types. This flexibility enables you to handle complex sorting scenarios and sort your data in a way that meets your requirements.

References:
- C++ Lambda Expressions: https://en.cppreference.com/w/cpp/language/lambda
- C++ Functors: https://en.cppreference.com/w/cpp/utility/functional/function