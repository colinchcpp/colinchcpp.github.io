---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [references]
comments: true
share: true
---

Sorting is a common operation in programming, widely used to arrange data in a specific order. In many cases, we can make use of the default sorting behavior provided by programming languages. However, there are scenarios where we need to sort data based on custom criteria or non-standard requirements. In this blog post, we will explore how to perform custom sorting using literals in C++.

## What are Sorting Literals?

In C++, sorting literals refer to the specific values or attributes used to determine the order of elements during the sorting process. By default, C++ provides sorting based on the natural order of the elements, such as ascending or descending order of numbers or lexicographical order of strings. However, in some cases, we may need to sort elements based on a different property or attribute.

## Creating Custom Sorting Literals

To create custom sorting literals in C++, we can make use of different sorting algorithms provided by the Standard Template Library (STL) or write our own sorting function. Let's take a look at an example that demonstrates how to sort a collection of strings based on their lengths.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to compare string lengths
bool compareStringLength(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cherry", "dragonfruit"};

    // Sorting strings based on length using custom sorting literal
    std::sort(strings.begin(), strings.end(), compareStringLength);

    // Displaying sorted strings
    for (const auto& str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the above code, we define a custom comparison function `compareStringLength` that takes two strings as arguments and compares their lengths. The `std::sort` function from the `<algorithm>` header is then used to sort the `strings` vector based on the lengths of the strings.

After sorting, the output will be: `apple cherry banana dragonfruit`. The elements are sorted based on their lengths, rather than the default lexicographic order.

## Conclusion

Custom sorting literals allow us to define our own criteria for sorting elements in C++. Whether it's sorting based on custom properties, attributes, or any other criteria, we can implement custom comparison functions to achieve the desired sorting behavior.

By using custom sorting literals, we can tailor our sorting algorithms to the specific needs of our application. It grants us greater flexibility and control over the sorting process, ensuring that our data is ordered according to our requirements.

#references
- [C++ Standard Template Library documentation](https://en.cppreference.com/w/cpp/algorithm/sort)
- ["The C++ Programming Language" by Bjarne Stroustrup](https://www.stroustrup.com/programming.html)
- [GeeksforGeeks: Sorting Algorithms in C++](https://www.geeksforgeeks.org/cpp-sort-class-objects-using-operator/)