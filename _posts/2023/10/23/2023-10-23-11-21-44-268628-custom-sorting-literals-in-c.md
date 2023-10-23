---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In C++, when sorting elements in a collection using the `std::sort` algorithm, it is sometimes necessary to provide custom sorting criteria based on specific requirements. One common situation is when the default sorting order of literals doesn't meet our needs, and we want to define our own ordering.

Let's say we have a collection of strings and we want to sort them in a specific order - let's say "apple" should come before "banana," but after "orange." In this case, we need to define our own custom sorting literals.

To achieve this, we can make use of a lambda function as the comparison criterion for the `std::sort` algorithm. Here's an example of how we can implement custom sorting literals in C++:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    // Define the custom sorting literals
    auto customOrder = [](const std::string& a, const std::string& b) {
        static const std::vector<std::string> sortOrder = {"orange", "apple", "banana"};

        auto aPos = std::find(sortOrder.begin(), sortOrder.end(), a);
        auto bPos = std::find(sortOrder.begin(), sortOrder.end(), b);

        return aPos < bPos;
    };

    // Create a vector of strings to sort
    std::vector<std::string> fruits = {"orange", "banana", "apple"};

    // Sort the vector using the custom sorting literals
    std::sort(fruits.begin(), fruits.end(), customOrder);

    // Print the sorted vector
    for (const auto& fruit : fruits) {
        std::cout << fruit << " ";
    }

    return 0;
}
```

In this code, we define a lambda function `customOrder` that compares two strings based on our custom sorting order. We create a `sortOrder` vector that contains the desired order of the literals. The lambda function uses `std::find` to find the positions of the two strings within the `sortOrder` vector, and returns `true` if `a` should come before `b` in the custom sorting order.

We then use `std::sort` to sort the vector of strings `fruits` using our custom sorting literals defined by the `customOrder` lambda function. Finally, we print the sorted vector to verify the sorting results.

By providing our own custom sorting literals, we have full control over the sorting order and can tailor it to meet our specific requirements.

Writing custom sorting literals in C++ can be incredibly useful when dealing with complex sorting scenarios. It allows us to sort elements in a way that is meaningful for our application and enables greater flexibility in organizing and manipulating data.

# Conclusion

Custom sorting literals in C++ provide a powerful mechanism for defining specific sorting orders based on our application's needs. By using a lambda function as the comparison criterion and defining our desired sorting order, we can easily implement custom sorting in C++. This allows us to sort elements in a way that makes sense for our specific use cases, increasing the versatility and adaptability of our code.

# References

- [C++ Reference - std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Reference - std::vector](https://en.cppreference.com/w/cpp/container/vector)
- [C++ Reference - Lambda functions](https://en.cppreference.com/w/cpp/language/lambda)