---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

When working with arrays or vectors in C++, the default sorting order is often based on the built-in comparison operators of the data type. However, there might be cases where you need to define a custom sorting order based on certain criteria. In such situations, you can utilize custom sorting literals to override the default behavior.

## Implementing Custom Sorting Order

To implement a custom sorting order, you need to define a comparison function or lambda expression that compares elements according to your desired criteria. The comparison function should return a Boolean value, indicating whether the first element is considered smaller than the second element.

Here's an example that demonstrates how to sort a vector of strings based on their lengths in ascending order:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareByLength(const std::string& a, const std::string& b) {
    return a.length() < b.length();
}

int main() {
    std::vector<std::string> words = { "apple", "banana", "cherry", "date" };

    // Sort the vector based on length
    std::sort(words.begin(), words.end(), compareByLength);

    // Print the sorted vector
    for (const auto& word : words) {
        std::cout << word << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, we define a comparison function `compareByLength` that compares two strings based on their lengths. The `std::sort` algorithm is then used to sort the vector of words using the `compareByLength` function as the custom sorting literal. Finally, we print the sorted vector to verify the results.

## Custom Sorting with Lambda Expressions

Instead of defining a named function for the custom sorting literal, we can use lambda expressions to define the comparison logic inline. This results in more concise code. Let's modify the previous example to use a lambda expression:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::string> words = { "apple", "banana", "cherry", "date" };

    // Sort the vector based on length using a lambda expression
    std::sort(words.begin(), words.end(), [](const std::string& a, const std::string& b) {
        return a.length() < b.length();
    });

    // Print the sorted vector
    for (const auto& word : words) {
        std::cout << word << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, we directly define a lambda expression as the custom sorting literal within the `std::sort` function call. The lambda expression compares two strings based on their lengths.

## Conclusion

Custom sorting literals provide a way to sort elements in a specific order defined by your own comparison criteria. Whether using a named function or a lambda expression, you can override the default sorting behavior to achieve the desired result. Custom sorting literals are useful when you need to sort elements based on non-standard attributes or properties.

#References

- [C++ std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [Lambda Expressions in C++](https://en.cppreference.com/w/cpp/language/lambda)