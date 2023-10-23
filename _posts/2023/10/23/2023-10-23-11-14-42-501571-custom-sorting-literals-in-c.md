---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In C++, sorting a list of elements is a common task. The standard library provides several sorting algorithms, such as `std::sort`, that can be used to sort elements in ascending order. However, what if you need to sort elements in a custom order, based on specific literals?

One solution is to provide a custom sorting function or functor that defines the desired order of elements. This can be achieved by overloading the comparison operators for the type of elements you want to sort.

Let's consider a simple example. Suppose we have a list of colors represented by strings, and we want to sort them in a custom order: "red", "green", "blue". 

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int customCompare(const std::string& a, const std::string& b) {
    std::vector<std::string> order = { "red", "green", "blue" };
    auto itA = find(order.begin(), order.end(), a);
    auto itB = find(order.begin(), order.end(), b);
    
    if (itA != order.end() && itB != order.end()) {
        return std::distance(order.begin(), itA) < std::distance(order.begin(), itB);
    }
    
    // Handle elements not present in the order list
    return a < b;
}

int main() {
    std::vector<std::string> colors = { "blue", "red", "green", "blue", "red", "green" };
    std::sort(colors.begin(), colors.end(), customCompare);
    
    for (const auto& color : colors) {
        std::cout << color << " ";
    }
    
    return 0;
}
```

In the code above, we define a custom comparison function `customCompare` that takes two strings `a` and `b` as input. We create a vector `order` that defines the desired order of the elements. Then, we use the `std::find` algorithm to find the positions of elements `a` and `b` in the `order` vector. If both elements are found, we compare their positions to determine the order. If one or both elements are not found, we use the default lexicographical comparison (`<`) as a fallback.

In the `main` function, we create a vector `colors` with a mix of red, green, and blue colors. We use `std::sort` to sort the vector based on the custom order defined by `customCompare`. Finally, we iterate through the sorted vector and print the colors.

The output of the above code will be: "red red green green blue blue".

By providing a custom comparison function or functor, you can sort elements in any desired order based on specific literals. This approach allows you to have full control over the sorting logic and enables you to sort elements in a way that best suits your needs.

---

References:
- [std::sort - cppreference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [std::find - cppreference](https://en.cppreference.com/w/cpp/algorithm/find)