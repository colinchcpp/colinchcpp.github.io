---
layout: post
title: "Improved structured bindings"
description: " "
date: 2023-09-29
tags: [structured]
comments: true
share: true
---

In C++20, structured bindings have been enhanced to offer even more flexibility and convenience. Here are some of the improvements that have been introduced:

1. **Support for non-constant expressions**: In C++20, structured bindings can be used with non-constant expressions. This means we can now use structured bindings with objects that are not declared as `const`. This allows for better code organization and flexibility.

```cpp
std::map<int, std::string> students{{1, "John"}, {2, "Alice"}, {3, "Bob"}};

for (auto& [id, name] : students) {
    name += " Doe";
}
```

2. **Initializer list support**: C++20 allows structured bindings to be used with initializer lists. This means that we can easily decompose an initializer list into its individual elements without having to manually access them by index.

```cpp
std::vector<int> numbers{1, 2, 3, 4, 5};

auto [a, b, c, d, e] = numbers;
```

3. **Ignored bindings**: In previous versions of C++, all members of a structure had to be bound to a variable, even if we were not interested in using them. With C++20, we can choose to ignore certain members using an underscore `_` as the variable name.

```cpp
std::pair<int, int> point{1, 2};

auto [x, _] = point; // Ignore the second component

std::tuple<int, float, std::string> data{42, 3.14f, "Hello"};

auto [value, _, message] = data; // Ignore the second element
```

4. **Refinements for arrays**: In C++20, structured bindings for arrays now support `std::size` and `std::data`. This allows us to decompose arrays and access their elements using structured bindings more easily.

```cpp
int array[5] = {1, 2, 3, 4, 5};

auto [first, second, third, fourth, fifth] = array;
```

Structured bindings have become even more powerful and flexible in C++20, making it easier to work with complex data structures. By taking advantage of these improvements, we can write cleaner and more expressive code.

#cpp #c++20 #structured-bindings