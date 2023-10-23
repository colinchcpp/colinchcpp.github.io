---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [sorting]
comments: true
share: true
---

Sorting is a fundamental operation in programming, and C++ provides the `std::sort` algorithm in the `<algorithm>` library for sorting elements in a given container. By default, this algorithm sorts elements in ascending order using the less than operator (`<`).

However, there may be scenarios where you want to customize the sorting order by defining your own comparing function or lambda expression. In this article, we'll explore how to use custom sorting literals in C++.

## Default Sorting

Let's begin with a simple example of sorting integers in ascending order using `std::sort`:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {3, 1, 4, 2, 5};

    std::sort(numbers.begin(), numbers.end());

    for (int num : numbers) {
        std::cout << num << " ";
    }

    return 0;
}
```

Output: `1 2 3 4 5`

In the above code, we have a vector of integers `numbers` and we use `std::sort` to sort them in ascending order. By default, `std::sort` uses the less than operator (`<`) to compare elements and arrange them accordingly.

## Custom Sorting Order

To define a custom sorting order, we need to pass a comparison function or lambda expression to `std::sort`. This function or lambda expression should return `true` if the first element is considered smaller than the second one based on the custom criterion.

Let's consider an example where we want to sort a vector of strings based on the length of the strings:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool lengthComparator(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "orange"};

    std::sort(words.begin(), words.end(), lengthComparator);

    for (const std::string& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

Output: `apple cherry banana orange`

In the above code, we define a custom comparison function `lengthComparator` that compares two strings based on their lengths. We then pass this function as the third parameter to `std::sort`. As a result, the vector of strings `words` is sorted based on the length of the strings.

## Using Lambda Expressions

C++ also allows us to use lambda expressions instead of separate comparison functions to define custom sorting order. Let's modify the previous example to sort the strings in descending order of their lengths:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::string> words = {"apple", "banana", "cherry", "orange"};

    std::sort(words.begin(), words.end(), [](const std::string& str1, const std::string& str2) {
        return str1.length() > str2.length();
    });

    for (const std::string& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

Output: `banana orange cherry apple`

In this example, we define a lambda expression directly inside the `std::sort` call, which compares two strings based on their lengths using the greater than operator (`>`). As a result, the strings are sorted in descending order of their lengths.

## Conclusion

In C++, you can customize the sorting order of elements by defining your own comparison function or lambda expression and passing it to the `std::sort` algorithm. This allows you to sort elements based on any criteria you desire, providing flexibility and control over your sorting operations.

By using custom sorting literals, you can manipulate the sorting order to suit your specific needs, making your code more expressive and efficient.

For more information, you can refer to the [C++ documentation on `std::sort`](https://en.cppreference.com/w/cpp/algorithm/sort).

#cpp #sorting