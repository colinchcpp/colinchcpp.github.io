---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [references]
comments: true
share: true
---

Sorting is a common operation in programming, allowing us to arrange elements in a specific order. In many cases, we can use the default sorting order for the data types we work with. However, there are scenarios in which we need to sort elements using a custom order that is not built into the language.

C++ provides a powerful mechanism to achieve custom sorting using sorting literals. Sorting literals allow us to define a specific order for elements based on our requirements. In this blog post, we will explore how to implement custom sorting literals in C++.

## Defining a Custom Sorting Order

To define a custom sorting order, we need to provide a comparison function that compares two elements and returns whether they should be swapped or not. C++ provides the `sort` algorithm from the `<algorithm>` library, which we can use with a custom comparison function to achieve this.

Here's an example of defining a custom sorting order for a vector of strings in C++, where we want to sort the strings based on their lengths:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool customSort(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "orange", "grapefruit"};

    std::sort(strings.begin(), strings.end(), customSort);

    for (const auto& str : strings) {
        std::cout << str << " ";
    }

    return 0;
}
```

In this example, the `customSort` function compares two strings based on their lengths. The `sort` algorithm uses this function to arrange the strings in ascending order of length.

The output of the above code will be: `apple orange banana grapefruit`.

## Lambda Functions for Custom Sorting

In addition to defining a separate comparison function, C++ also provides a convenient way to define custom sorting using lambda functions. Lambda functions allow us to define functions inline without explicitly declaring them separately.

Here's an example of using a lambda function to achieve the same custom sorting order as before:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::string> strings = {"apple", "banana", "orange", "grapefruit"};

    std::sort(strings.begin(), strings.end(), [](const std::string& str1, const std::string& str2) {
        return str1.length() < str2.length();
    });

    for (const auto& str : strings) {
        std::cout << str << " ";
    }

    return 0;
}
```

Both examples produce the same output, allowing us to sort the strings based on their lengths.

## Conclusion

Custom sorting literals provide flexibility when it comes to sorting elements using a specific ordering that is not available by default. In C++, we can achieve this functionality by defining a custom comparison function or by using lambda functions.

By utilizing custom sorting literals, we can easily adapt sorting operations to fit various requirements in our programs.

#references
- [C++ sort - cppreference.com](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ lambda functions - cppreference.com](https://en.cppreference.com/w/cpp/language/lambda)