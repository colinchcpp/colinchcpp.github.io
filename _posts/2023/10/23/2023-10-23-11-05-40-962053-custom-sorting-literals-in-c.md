---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with collections in C++, it's often necessary to sort the elements based on certain criteria. By default, the sorting order is based on the natural order of the elements. However, there may be cases where we want to define a custom sorting order based on our own criteria.

In C++, we can achieve this by using custom sorting literals. Custom sorting literals allow us to define a custom order for the elements in a collection, overriding the default comparison mechanism.

Let's consider an example where we have a collection of strings and we want to sort them based on their length in descending order. Here's how we can do it using custom sorting literals in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareLength(const std::string& a, const std::string& b) {
    return a.length() > b.length();
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cherry", "durian"};

    std::sort(strings.begin(), strings.end(), compareLength);

    for(const auto& str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the above code, we define a custom comparison function `compareLength` that compares two strings based on their length. The function returns `true` if the length of the first string is greater than the second string. 

We then pass this comparison function to the `std::sort` algorithm as the third parameter. This tells the `std::sort` algorithm to use our custom sorting order instead of the default comparison.

The output of the above code will be:
```
banana cherry durian apple 
```

Here, the strings are sorted based on their lengths in descending order.

By using custom sorting literals, we have the flexibility to define our own criteria for sorting elements in C++. It allows us to customize the sorting order based on the specific requirements of our application.

Now, let's recap the key points of custom sorting literals in C++:

- Custom sorting literals allow us to define a custom order for sorting elements in a collection.
- We can define a custom comparison function and pass it as a parameter to the sorting algorithm, overriding the default comparison mechanism.
- Custom sorting literals provide us with flexibility in defining sorting criteria based on our specific needs.

# References
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [Custom Sort Order for a Vector in C++](https://stackoverflow.com/questions/1380463/custom-sort-order-for-a-vector-in-c)