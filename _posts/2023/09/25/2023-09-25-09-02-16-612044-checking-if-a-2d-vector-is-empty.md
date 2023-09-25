---
layout: post
title: "Checking if a 2D vector is empty"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

## Checking for an Empty 2D Vector in Python

Python provides a simple way to check if a 2D list (which can be considered as a 2D vector) is empty. You can use the `not` operator to check if the list has any elements.

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
is_empty = not matrix
print(is_empty)  # False

empty_matrix = []
is_empty = not empty_matrix
print(is_empty)  # True
```

In the above example, the `not` operator is used to check if the `matrix` list is empty. If it yields `True`, it means the matrix is empty. In this case, it will print `False` because the matrix has elements. The same applies to the `empty_matrix` list, which is empty, so it will print `True`.

## Checking for an Empty 2D Vector in C++

In C++, checking if a 2D vector is empty involves using the `empty()` function provided by the `std::vector` library. Here's an example:

```cpp
{% raw %}
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    bool is_empty = matrix.empty();
    std::cout << std::boolalpha << is_empty << std::endl;  // false

    std::vector<std::vector<int>> empty_matrix;
    is_empty = empty_matrix.empty();
    std::cout << std::boolalpha << is_empty << std::endl;  // true

    return 0;
}
{% endraw %}
```

In the C++ example, the `empty()` function is used to check if `matrix` and `empty_matrix` are empty or not. The function returns `true` if the vector is empty and `false` otherwise. By using `std::boolalpha` with `std::cout`, we print `true` and `false` instead of `1` and `0`, respectively.

## Conclusion

By using the appropriate methods provided by your programming language, you can easily check if a 2D vector is empty. In Python, you can utilize the `not` operator, while in C++, you can use the `empty()` function.