---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References, reference]
comments: true
share: true
---

When working with sorting algorithms in C++, you may often encounter the need to define a custom order for certain literals or values. For example, sorting a list of strings in a dictionary-like order or sorting a list of integers based on some specific criteria.

In C++, the `std::sort` function from the `<algorithm>` library is commonly used for sorting elements in a container. By default, it sorts elements in ascending order using the less-than (`<`) operator. However, it does not provide direct support for sorting elements based on custom literals.

To achieve custom sorting, you can either define a custom comparator function or overload the less-than operator (`<`) for your type. Let's explore both approaches.

## 1. Custom Comparator Function
A custom comparator function allows you to specify the criteria for sorting elements. The function should return `true` if the first element should come before the second element, and `false` otherwise.

Here's an example of sorting a vector of strings using a custom comparator function to achieve dictionary-like order:

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

bool dictionarySort(const std::string& a, const std::string& b) {
    return a < b;
}

int main() {
    std::vector<std::string> words = {"apple", "banana", "cat", "dog"};

    std::sort(words.begin(), words.end(), dictionarySort);

    for (const auto& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

The `dictionarySort` function compares two strings using the less-than operator (`<`). Running this code will output: `apple banana cat dog`.

## 2. Overloading the Less-Than Operator
An alternative approach is to overload the less-than (`<`) operator for your type. This allows you to define the custom sorting criteria directly within the type definition.

Here's an example of sorting a vector of integers based on their absolute values:

```cpp
{% raw %}
#include <algorithm>
#include <vector>
#include <iostream>
#include <cmath>

struct CustomInt {
    int value;
    
    // Overload the less-than operator
    bool operator<(const CustomInt& other) const {
        return std::abs(value) < std::abs(other.value);
    }
};

int main() {
    std::vector<CustomInt> numbers = {{-5}, {2}, {-10}, {7}};

    std::sort(numbers.begin(), numbers.end());

    for (const auto& number : numbers) {
        std::cout << number.value << " ";
    }

    return 0;
}
{% endraw %}
```

In this example, the `CustomInt` struct overloads the less-than operator (`<`), comparing the absolute values of the `value` member. Running this code will output: `-2 -5 7 -10`.

By providing a custom comparator function or overloading the less-than operator, you can easily customize how elements are sorted to meet specific requirements.

Remember to tailor the approach based on your specific needs, and explore other sorting algorithms available in the `<algorithm>` library for more complex sorting tasks.

## Conclusion
Sorting elements based on custom literals or values is a common requirement in programming. In C++, you can achieve this by either defining a custom comparator function or overloading the less-than operator for your type. Both methods offer flexibility and allow you to customize the sorting criteria to meet your specific needs.

#References [#reference] 
- [std::sort - cppreference.com](https://en.cppreference.com/w/cpp/algorithm/sort)
- [How to overload operators in C++ - GeeksforGeeks](https://www.geeksforgeeks.org/operator-overloading-c/)

[#cplusplus] #C++ #Sorting