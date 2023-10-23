---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a fundamental operation in programming and sometimes we need to sort elements based on custom criteria. In C++, we can achieve this by using custom sorting literals. Custom sorting literals allow us to define our own comparison rules when sorting elements in a container.

## Sorting with Standard Comparators

Before we dive into custom sorting literals, let's quickly review how sorting works with standard comparators in C++. To sort elements in ascending order, we can use the `std::sort` function from the `<algorithm>` library along with the less than operator (`<`) as the comparator.

```cpp
#include <algorithm>
#include <vector>

bool compare(int a, int b) {
    return a < b;
}

int main() {
    std::vector<int> numbers = {5, 2, 3, 1, 4};
    std::sort(numbers.begin(), numbers.end(), compare);

    // Print sorted numbers
    for (int num : numbers) {
        std::cout << num << " ";
    }

    return 0;
}
```

Output: `1 2 3 4 5`

In this example, we define the `compare` function as our custom comparator, which compares two integers using the less than operator. The `std::sort` function uses this comparator to sort the elements in the `numbers` vector.

## Custom Sorting Literals

Custom sorting literals provide a more concise and expressive way to define comparison rules directly in the sorting statement. They make the code more readable and reduce the need for separate comparator functions.

To use custom sorting literals, we need to define them as lambda functions. Lambda functions are anonymous functions that can be defined inline and capture variables from their surrounding scope. They are denoted by the `[]` square brackets and followed by a function body.

Let's rewrite the previous example using custom sorting literals:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {5, 2, 3, 1, 4};
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) { return a < b; });

    // Print sorted numbers
    for (int num : numbers) {
        std::cout << num << " ";
    }

    return 0;
}
```

Output: `1 2 3 4 5`

In this updated code, we define the custom sorting literal directly inside the `std::sort` function call. The lambda function `[](int a, int b) { return a < b; }` serves as the custom comparator and defines the sorting criteria.

## Using Custom Sorting Criteria

The real power of custom sorting literals comes from the flexibility they offer in defining custom sorting criteria. We can easily modify the lambda function to implement different comparison rules.

For example, let's sort a list of strings based on their lengths in descending order:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<std::string> words = {"apple", "banana", "cat", "dog", "elephant"};
    std::sort(words.begin(), words.end(), [](const std::string& a, const std::string& b) {
        return a.length() > b.length();
    });

    // Print sorted words
    for (const std::string& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

Output: `elephant banana apple cat dog`

In this example, we define a lambda function `[](const std::string& a, const std::string& b) { return a.length() > b.length(); }` as the custom comparator. It compares two strings based on their length, sorting them in descending order.

## Conclusion

Custom sorting literals in C++ provide a concise and flexible way to define custom comparison rules when sorting elements. By using lambda functions as custom comparators, we can implement sorting criteria inline, making our code more readable and reducing the need for separate comparator functions.

Using custom sorting literals is especially helpful when sorting elements based on complex or custom conditions. They enhance the expressiveness and maintainability of our code, making it easier to understand the sorting logic.

# References
- [C++ Reference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Reference - Lambda Expressions](https://en.cppreference.com/w/cpp/language/lambda)