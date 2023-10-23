---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [cplusplus, sorting]
comments: true
share: true
---

Sorting is a common operation in programming, and most programming languages provide built-in functions for sorting data structures like arrays or lists. However, there are situations where the default sorting order may not be suitable. In such cases, you may need to implement custom sorting logic to achieve the desired results.

In C++, you can customize the sorting order by defining your own comparison function or using lambda expressions. In this blog post, we'll explore both approaches and demonstrate how to sort literals in a custom order.

## Using a Comparison Function

One way to achieve custom sorting in C++ is by using a comparison function. The comparison function takes two elements as input and returns `true` if the first element should come before the second element in the sorted result, and `false` otherwise.

Let's say we have an array of string literals that we want to sort in a specific order. For example, we want to sort the strings "apple", "banana", "cherry", "date", and "kiwi" in the order "kiwi", "banana", "cherry", "date", "apple". Here's how we can accomplish this using a comparison function:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

bool customCompare(const std::string& a, const std::string& b) {
    std::vector<std::string> sortOrder = {"kiwi", "banana", "cherry", "date", "apple"};

    auto aIndex = std::find(sortOrder.begin(), sortOrder.end(), a) - sortOrder.begin();
    auto bIndex = std::find(sortOrder.begin(), sortOrder.end(), b) - sortOrder.begin();

    return aIndex < bIndex;
}

int main() {
    std::vector<std::string> fruits = {"banana", "apple", "kiwi", "cherry", "date"};

    std::sort(fruits.begin(), fruits.end(), customCompare);

    for (const auto& fruit : fruits) {
        std::cout << fruit << " ";
    }

    return 0;
}
```

In this example, we define a `customCompare` function that takes two string literals `a` and `b` and compares them based on their indices in the `sortOrder` vector. We then use this comparison function with the `std::sort` algorithm to sort the `fruits` vector in the desired order. The output of this program will be: "kiwi banana cherry date apple".

## Using Lambda Expressions

Another approach to custom sorting in C++ is to use lambda expressions. Lambda expressions allow you to define inline functions without explicitly naming them. They are especially useful when you want to define a comparison function on the spot.

Let's modify our previous example to use a lambda expression instead of a separate comparison function:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    std::vector<std::string> fruits = {"banana", "apple", "kiwi", "cherry", "date"};
  
    std::vector<std::string> sortOrder = {"kiwi", "banana", "cherry", "date", "apple"}; 

    std::sort(fruits.begin(), fruits.end(), [&](const std::string& a, const std::string& b) {
        auto aIndex = std::find(sortOrder.begin(), sortOrder.end(), a) - sortOrder.begin();
        auto bIndex = std::find(sortOrder.begin(), sortOrder.end(), b) - sortOrder.begin();
      
        return aIndex < bIndex;
    });

    for (const auto& fruit : fruits) {
        std::cout << fruit << " ";
    }

    return 0;
}
```

In this example, we define the `sortOrder` vector within the `main` function and use a lambda expression as the comparison function for `std::sort`. The lambda expression captures the `sortOrder` vector by reference and compares the two elements based on their indices in the `sortOrder` vector.

The output of this program will be the same as before: "kiwi banana cherry date apple".

## Conclusion

Custom sorting allows you to sort data in a specific order that is not provided by default sorting functions in C++. By using comparison functions or lambda expressions, you can define your own sorting logic and achieve the desired results.

Both the comparison function and lambda expression approaches are powerful and flexible, and you can choose the one that best fits your use case. Remember to carefully define your comparison logic to ensure correct sorting results.

I hope this blog post has provided you with a good understanding of how to implement custom sorting literals in C++. Happy coding!

\#cplusplus #sorting