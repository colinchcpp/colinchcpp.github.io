---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a fundamental operation in programming, and C++ provides various sorting algorithms to arrange elements in a particular order. However, sometimes you may encounter special cases where the default sorting mechanisms are not sufficient. In such scenarios, custom sorting literals can come to the rescue.

Custom sorting literals allow you to define your own criteria for sorting elements in C++. This is particularly useful when dealing with complex data structures or non-standard comparisons.

## How to Use Custom Sorting Literals

To make use of custom sorting literals in C++, you need to provide a custom comparison function or lambda expression. This function or lambda expression defines the sorting criteria for the elements.

Here is an example of using a custom sorting literal to sort a vector of strings in descending order of their lengths:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareByLength(const std::string& first, const std::string& second) {
    return first.length() > second.length();
}

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};

    std::sort(words.begin(), words.end(), compareByLength);

    for (const std::string& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

In this example, the `compareByLength` function compares two strings by their lengths and returns `true` if the first string is longer than the second.
The `std::sort` function takes the provided `compareByLength` function as the sorting criterion.

The output of the above code will be: `banana cherry apple date`.

## Using Lambda Expressions for Custom Sorting Literals

In addition to using functions, C++ also allows the use of lambda expressions as custom sorting literals. Lambda expressions provide a more concise way to define the comparison criterion inline.

Here is the modified version of the previous example using a lambda expression:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "date"};

    std::sort(words.begin(), words.end(), [](const std::string& first, const std::string& second){
        return first.length() > second.length();
    });

    for (const std::string& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

The output will be the same: `banana cherry apple date`.

## Conclusion

Custom sorting literals provide flexibility in sorting elements based on custom criteria in C++. By defining your own comparison function or using lambda expressions, you can easily sort elements according to your requirements. So, the next time you encounter a sorting scenario that is not handled by default sorting mechanisms, consider using custom sorting literals.