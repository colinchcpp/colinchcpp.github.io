---
layout: post
title: "Iterating over a 2D vector using loops"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

## Iterating over a 2D Vector in C++

In C++, you can iterate over a 2D vector using nested for loops. Here's an example:

```cpp
{% raw %}
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    for (int row = 0; row < matrix.size(); row++) {
        for (int col = 0; col < matrix[row].size(); col++) {
            std::cout << matrix[row][col] << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
{% endraw %}
```

In the above code, we use two nested for loops to iterate over each element in the 2D vector. The outer loop iterates over each row, and the inner loop iterates over each column within that row. We access the elements using `matrix[row][col]`, where `row` is the current row and `col` is the current column.

## Iterating over a 2D Vector in Python

In Python, iterating over a 2D vector is simplified using list comprehensions. Here's an example:

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for row in matrix:
    for col in row:
        print(col, end=" ")
    print()
```

In Python, we can directly iterate over the rows of the 2D vector. For each row, we can then iterate over the elements using a nested for loop. The `print()` statement with `end=" "` ensures that the elements are printed on the same line.

## Conclusion
In this blog post, we have learned how to iterate over a 2D vector using loops in C++ and Python. By understanding these methods, you can easily access and manipulate the elements within a 2D vector. Feel free to experiment with different scenarios and optimize your code for better performance!

#programming #2DVector #loops