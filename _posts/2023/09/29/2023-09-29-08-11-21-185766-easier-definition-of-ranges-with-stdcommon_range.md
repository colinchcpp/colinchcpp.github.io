---
layout: post
title: "Easier definition of ranges with std::common_range"
description: " "
date: 2023-09-29
tags: [include, include]
comments: true
share: true
---

Writing code that operates on ranges of values has become more streamlined and convenient in modern C++. The introduction of the ranges library in C++20 offers a plethora of algorithms and utilities to manipulate collections of elements effectively. One particularly helpful addition is the `std::common_range` concept, which simplifies the definition of ranges in a concise manner.

## What is `std::common_range`?

`std::common_range` is a concept specified in the C++20 standard library. It characterizes a type that models both the `std::ranges::range` and `std::ranges::sized_range` concepts. In other words, it represents a range that is both iterable and has a known size. The `std::common_range` concept is enabled for any type that satisfies these requirements.

The `std::ranges::range` concept ensures that a type can be iterated over, typically through the presence of member functions such as `begin()` and `end()`. On the other hand, the `std::ranges::sized_range` concept adds the capability to determine the number of elements in the range, enabling optimizations based on its size.

## Simplifying Range Definitions with `std::common_range`

The primary advantage of `std::common_range` is its ability to simplify the definition of ranges without explicitly specifying multiple concepts. By using this concept, we can reduce the verbosity and improve the readability of our code. Here's an example to demonstrate its usage:

```cpp
#include <iostream>
#include <ranges>
#include <vector>

void printRangeSize(std::common_range auto&& range)
{
    std::cout << "Range size: " << std::ranges::size(range) << std::endl;
}

int main()
{
    std::vector<int> numbers{1, 2, 3, 4, 5};
    printRangeSize(numbers);
    
    int array[] = {6, 7, 8, 9, 10};
    printRangeSize(array);

    return 0;
}
```

In the code snippet above, the `printRangeSize` function takes a parameter `range` of type `std::common_range auto&&`. This allows the function to accept any range that models the `std::common_range` concept, regardless of its specific type.

By using `std::common_range`, we avoid the need to define separate templates or overloads for different range categories. The `std::ranges::size` function also works seamlessly with `std::common_range`, enabling us to retrieve the size of the range regardless of whether it is a container, array, or a custom range type.

## Conclusion

The `std::common_range` concept introduced in C++20 simplifies the definition and handling of ranges in a concise and readable manner. By combining the features of both `std::ranges::range` and `std::ranges::sized_range`, it enables us to write more generic and efficient code when working with ranges. Consider leveraging `std::common_range` in your projects to improve code clarity and maintainability when dealing with ranges.

#cplusplus #rangelibrary