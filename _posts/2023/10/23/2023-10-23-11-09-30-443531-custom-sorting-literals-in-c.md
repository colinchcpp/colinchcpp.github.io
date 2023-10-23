---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

Sorting is a common task in programming, and in C++, we have several built-in sorting functions such as `std::sort` that work well for sorting standard data types. However, when it comes to custom sorting requirements, we often need to define our own comparison function or functors.

In some cases, the default sorting order of certain data types may not be suitable for our needs. For example, consider a case where we want to sort a list of strings containing numbers in lexicographical order rather than their usual numerical order.

To customize the sorting behavior, we can define our own comparison function or functor that takes into account our specific requirements. Let's take a look at an example:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <sstream>

// Custom sorting comparator
bool customSort(const std::string& a, const std::string& b) {
    // Extract numbers from strings
    std::stringstream sa(a);
    std::stringstream sb(b);
    
    int numA, numB;
    sa >> numA;
    sb >> numB;
    
    // Compare extracted numbers
    return numA < numB;
}

int main() {
    std::vector<std::string> numbers{"10", "5", "2", "100", "50"};

    // Sort the numbers using the custom sort function
    std::sort(numbers.begin(), numbers.end(), customSort);

    // Print the sorted numbers
    for (const std::string& num : numbers) {
        std::cout << num << " ";
    }
    
    return 0;
}
```

In the above example, we have a custom comparison function `customSort` that extracts the numbers from the strings and compares them. We then use this custom function as the third argument in the `std::sort` function to sort the strings based on our defined sorting criteria.

The output of the above code would be: `2 5 10 50 100`, which is in lexicographical order rather than the default numerical ordering.

By defining our own comparison function, we have the flexibility to customize the sorting behavior according to our specific needs.

## Conclusion

Custom sorting in C++ allows us to sort data types based on our own defined criteria. By providing a custom comparison function or functor, we can sort data in a way that is different from the default sorting behavior. This flexibility enables us to handle unique sorting requirements efficiently.

#References
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Custom Comparators](https://www.geeksforgeeks.org/functors-in-cpp/)