---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with sorting algorithms in C++, it's common to sort elements in ascending or descending order based on their natural order defined by the data type. However, there may be cases where you want to sort elements based on a custom order or a specific criteria that is not provided by default. In such scenarios, you can define custom sorting literals to achieve the desired behavior.

## Defining Custom Sorting Literals

To define custom sorting literals in C++, you can use the `std::sort` algorithm along with a custom comparison function or lambda expression. The comparison function or lambda expression should define the specific order of the elements based on your custom criteria.

Consider the following example where we want to sort a vector of strings based on the length of the strings:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareLength(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> strings = {"apple", "orange", "banana", "kiwi"};

    // Sorting using custom comparison function
    std::sort(strings.begin(), strings.end(), compareLength);

    // Printing sorted strings
    for (const auto& str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `compareLength` function is used as the custom comparison function. It takes two `std::string` objects and compares their lengths. The `std::sort` algorithm uses this function to sort the `strings` vector based on the length of the strings.

The output of the above code will be:

```
kiwi apple banana orange
```

## Using Lambda Expressions

Alternatively, you can use lambda expressions to define the custom comparison directly inline:

```cpp
std::vector<std::string> strings = {"apple", "orange", "banana", "kiwi"};

// Sorting using lambda expression
std::sort(strings.begin(), strings.end(), [](const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
});

// Printing sorted strings
for (const auto& str : strings) {
    std::cout << str << " ";
}
std::cout << std::endl;
```

The output will be the same as before:

```
kiwi apple banana orange
```

## Conclusion

In scenarios where the default comparison provided by the C++ data types does not satisfy your sorting requirements, you can define custom sorting literals using custom comparison functions or lambda expressions. This allows you to sort elements based on your desired criteria and achieve the desired sorting order.

# References
- [std::sort - cppreference.com](https://en.cppreference.com/w/cpp/algorithm/sort)