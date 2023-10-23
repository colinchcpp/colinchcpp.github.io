---
layout: post
title: "Custom sorting literals in C++"
description: " "
date: 2023-10-23
tags: [cplusplus, sorting]
comments: true
share: true
---

Sorting is a common operation in programming, allowing us to arrange elements in a specific order. In C++, the `std::sort` function from the `<algorithm>` header is used to perform sorting on a range of elements. By default, `std::sort` uses the less-than (`<`) operator for comparison. However, there may be cases where we need to customize the sorting logic based on our own criteria.

In this blog post, we will explore how to perform custom sorting of literals in C++. Let's get started!

## Custom Sorting with Functors

A common way to implement custom sorting is by using functors (function objects) with overloaded `operator()` for comparison. First, we define a functor class that encapsulates our custom comparison logic. Let's say we want to sort strings based on their length. Here's an example:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

struct StringLengthComparator {
    bool operator()(const std::string& s1, const std::string& s2) const {
        return s1.length() < s2.length();
    }
};

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cherry", "date"};
    std::sort(strings.begin(), strings.end(), StringLengthComparator());

    for (const auto& str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the code above, we define the `StringLengthComparator` functor that compares two strings based on their lengths. We pass an instance of this functor class to `std::sort` as the third argument.

When we run the code, the output will be: `date apple cherry banana`. The strings are sorted in ascending order based on their lengths.

## Custom Sorting with Lambdas

Since C++11, we also have the option to use lambda expressions for custom sorting. Lambdas allow us to define anonymous functions inline, making the code more concise. Let's modify the previous example to use a lambda expression:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cherry", "date"};
    std::sort(strings.begin(), strings.end(),
              [](const std::string& s1, const std::string& s2) {
                  return s1.length() < s2.length();
              });

    for (const auto& str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code, we define a lambda function as the comparison criterion directly inside the `std::sort` call. The lambda expression takes two `const std::string&` parameters and compares their lengths. Again, the output will be: `date apple cherry banana`.

## Conclusion

Custom sorting literals in C++ is straightforward using functors or lambda expressions. By defining our own comparison logic, we can sort elements based on criteria other than the less-than operator. Functors are flexible and reusable, while lambdas provide a concise way to define comparison logic inline.

Using the examples and concepts discussed in this blog post, you can now easily implement custom sorting of literals in your C++ programs. Happy coding!

\#cplusplus #sorting