---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Sorting is a common task in programming when working with data structures like arrays or vectors. In many cases, the default sorting logic provided by the programming language may not be sufficient. In such cases, it becomes necessary to use custom sorting literals to sort the data according to our specific requirements.

In C++, the `std::sort` function from the `<algorithm>` header is commonly used to sort containers like vectors or arrays. By default, `std::sort` uses the less-than operator (`<`) to compare elements for sorting.

To customize the sorting logic, we can define our own comparison function or use lambda expressions.

## Custom Comparison Function

A comparison function is a function that takes two elements and returns a boolean value indicating whether the first element should come before the second element in the sorted order.

Here's an example of a custom comparison function that sorts strings in reverse alphabetical order:

```cpp
bool reverseStringSort(const std::string& a, const std::string& b) {
    return a > b;
}

int main() {
    std::vector<std::string> names = { "Alice", "Bob", "Charlie", "David" };

    std::sort(names.begin(), names.end(), reverseStringSort);

    for(const auto& name : names) {
        std::cout << name << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the above example, the `reverseStringSort` function returns `true` if `a` should come before `b` to sort the strings in reverse alphabetical order. This custom comparison function is then passed as the third parameter to `std::sort`.

## Lambda Expressions

Lambda expressions provide a concise way to define functions inline. They are useful when you need a custom sorting logic that is not reusable or too simple to define a separate function.

Here's an example using a lambda expression to sort integers in ascending order:

```cpp
int main() {
    std::vector<int> numbers = { 5, 2, 8, 1, 4 };

    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a < b;
    });

    for(const auto& number : numbers) {
        std::cout << number << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the lambda expression `[](int a, int b) { return a < b; }` defines a comparison function that returns `true` if `a` should come before `b`, sorting the numbers in ascending order.

## Conclusion

Custom sorting literals in C++ allow us to sort data according to our specific requirements. By defining custom comparison functions or using lambda expressions, we can tailor the sorting logic to our needs.

Using custom sorting literals expands the versatility of the `std::sort` function and enables us to effortlessly sort data in various ways.

# References
- [std::sort - C++ Reference](https://en.cppreference.com/w/cpp/algorithm/sort)
- [C++ Lambdas - GeeksforGeeks](https://www.geeksforgeeks.org/lambda-expression-in-c/)