---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [cplusplus, sorting]
comments: true
share: true
---

When working with arrays or vectors in C++, there may be times when you need to sort elements based on a specific criterion that is not supported by the default sorting order. In such cases, you can use custom sorting literals to define your own sorting logic.

## Sorting Based on Custom Criteria

To sort elements based on a custom criterion, you will need to define a function or a lambda expression that compares two elements and returns a bool value indicating their relative order.

Here's an example that demonstrates sorting a vector of strings in descending order of their lengths:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareLength(const std::string& s1, const std::string& s2) {
    return s1.length() > s2.length();
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cherry", "date"};
    
    std::sort(strings.begin(), strings.end(), compareLength);
    
    for (const auto& str : strings) {
        std::cout << str << " ";
    }
    
    return 0;
}
```

In the above example, we define the `compareLength` function that compares two strings based on their lengths. The `std::sort` function is then used with `compareLength` as the comparison function to sort the vector in descending order of string lengths.

## Sorting with Lambda Expressions

Alternatively, you can use lambda expressions to define the custom sorting logic inline without the need to define a separate function. Here's an example that sorts a vector of integers in ascending order of their absolute values:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {5, -3, 2, -8, 1};
    
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return std::abs(a) < std::abs(b);
    });
    
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }
    
    return 0;
}
```

In this example, the lambda expression `[](int a, int b) { return std::abs(a) < std::abs(b); }` is used as the comparison function to sort the vector of integers in ascending order of their absolute values.

## Conclusion

Using custom sorting literals in C++ allows you to sort elements based on criteria that are not supported by the default sorting order. You can either define a separate comparison function or use lambda expressions to provide the sorting logic inline. This flexibility makes it easy to sort elements in a way that suits your specific needs.

Check out the official documentation on [std::sort](https://en.cppreference.com/w/cpp/algorithm/sort) for more information on sorting in C++.

#cplusplus #sorting