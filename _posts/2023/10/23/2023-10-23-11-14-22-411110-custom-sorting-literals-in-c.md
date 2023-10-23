---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with arrays or vectors in C++, sorting the elements in a specific order is a common requirement. By default, the `std::sort` function in the C++ Standard Library sorts in ascending order using the `<` operator. However, sometimes we may need to sort elements using a different criterion. In these cases, we can use custom sorting literals to define our own sorting rules.

To illustrate this, let's consider a scenario where we have a vector of strings that we want to sort based on the length of the strings.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

bool compareStringLength(const std::string& str1, const std::string& str2) {
    return str1.length() < str2.length();
}

int main() {
    std::vector<std::string> words = {"apple", "orange", "banana", "kiwi"};

    std::sort(words.begin(), words.end(), compareStringLength);

    for (const auto& word : words) {
        std::cout << word << " ";
    }

    return 0;
}
```

In the above example, we declare a function `compareStringLength` that takes two strings as parameters and returns `true` if the length of the first string is less than the length of the second string. In the `main` function, we pass this function as the third argument to the `std::sort` function. This tells `std::sort` to use our custom sorting criterion.

The output of the program will be:

```
kiwi apple orange banana
```

As we can see, the elements are sorted based on their lengths in ascending order.

By defining custom sorting literals, we have the flexibility to sort elements according to any criterion we desire. This can be particularly useful when dealing with complex data structures or user-defined types where the default comparison operators may not provide the desired sorting logic.

# Conclusion
In C++, the `std::sort` function provides a convenient way to sort elements in a collection. By using custom sorting literals, we can define our own sorting rules, allowing us to sort elements based on any criterion we choose. This capability enhances the flexibility and extensibility of our code, enabling us to solve a wide range of sorting problems efficiently.