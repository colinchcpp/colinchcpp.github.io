---
layout: post
title: "Support for three-way comparisons in range adaptors"
description: " "
date: 2023-09-29
tags: [include, include]
comments: true
share: true
---

In the world of range-based programming, where iterators and adaptors play a crucial role in manipulating and transforming data, the introduction of three-way comparisons opens up new possibilities for efficient and expressive code. This blog post explores how range adaptors can benefit from the support for three-way comparisons in modern programming languages.

Three-way comparisons, also known as the spaceship operator (`<=>`), provide a concise way to compare two values and obtain a result that represents their relative ordering. Traditionally, two-way comparisons with relational operators (`<`, `<=`, `==`, `>=`, `>`) were used, but they had limitations when dealing with non-equivalent values. Three-way comparisons address these limitations by returning three possible outcomes: less than, equal to, or greater than.

## Improved sorting with `sort` range adaptor

The `sort` range adaptor is a common tool used to reorder elements within a range. With support for three-way comparisons, the `sort` adaptor can now achieve greater efficiency and accuracy when sorting ranges. By default, `sort` makes use of the `<` operator for comparisons, but it can leverage the three-way comparison operator for more fine-grained sorting.

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers{5, 2, 3, 1, 4};
    std::ranges::sort(numbers, std::ranges::less{});

    for (const auto& number : numbers) {
        std::cout << number << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

In the above example, the `sort` range adaptor uses `std::ranges::less{}` as a comparator. The `std::ranges::less{}` comparator leverages the three-way comparison operator to perform a more efficient and accurate sorting of the `numbers` range.

## Filtering with `filter` range adaptor

The `filter` range adaptor is another useful tool for selecting elements in a range based on a specific condition. With three-way comparisons, the `filter` adaptor can perform more advanced filtering operations. For example, consider the following code snippet:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers{5, 2, 3, 1, 4};
    std::ranges::filter_view filteredNumbers{numbers, [](const auto& n) {
        return n <=> 3 != std::strong_ordering::greater;
    }};

    for (const auto& number : filteredNumbers) {
        std::cout << number << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

In this example, the `filter` range adaptor is used in conjunction with the three-way comparison operator (`<=>`) to filter out all the elements greater than 3. The `filter_view` created by the `filter` adaptor only includes elements that satisfy the provided condition.

## Conclusion

The support for three-way comparisons in range adaptors greatly enhances the power and expressiveness of range-based programming. With the ability to leverage the spaceship operator (`<=>`), operations such as sorting and filtering become more efficient and accurate. By embracing the new features offered by modern programming languages, developers can write cleaner and more concise code when working with ranges and adaptors.

#techblog #rangeadaptors