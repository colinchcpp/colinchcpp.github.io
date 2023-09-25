---
layout: post
title: "Erasing elements at a specific position in a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

When working with a 2D vector in C++ and you need to remove elements at a specific position, you can use the `erase` function from the `<vector>` library. This function allows you to delete elements from a vector based on their position.

Here's an example code snippet demonstrating how to erase elements at a specific position in a 2D vector:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    // Remove the element at position (1, 1)
    matrix[1].erase(matrix[1].begin() + 1);

    // Print the updated 2D vector
    for (auto row : matrix) {
        for (auto element : row) {
            std::cout << element << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

In this code, we have a 2D vector `matrix` containing the numbers 1 to 9 arranged in a 3x3 grid. We want to remove the element at position (1, 1), which corresponds to the number 5. 

To achieve this, we use the `erase` function on the inner vector `matrix[1]`, which represents the second row. We pass the iterator pointing to the position we want to erase, in this case, `matrix[1].begin() + 1`, which is the element at index 1. This removes the number 5 from the second row.

Finally, we print the updated 2D vector to verify that the element has been successfully erased. The output will be:

```
1 2 3
4 6
7 8 9
```

By utilizing the `erase` function on a specific position, you can easily remove elements from a 2D vector in C++. Remember to pay attention to the indexing and handle the removed elements accordingly in your code.

#C++ #2DVector