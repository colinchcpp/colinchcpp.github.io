---
layout: post
title: "Using iterators with 2D vectors"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

Iterators are powerful tools in programming that allow us to traverse and manipulate the elements of containers, such as vectors. In this blog post, we'll explore how to use iterators with 2D vectors.

## What are 2D Vectors?

A 2D vector, also known as a vector of vectors, is essentially a vector in which each element is itself a vector. This data structure is useful when we need to represent a grid or a matrix.

Here's an example of how to declare and initialize a 2D vector in C++:

```cpp
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Rest of the code
}
```

## Accessing Elements of a 2D Vector with Iterators

To access the elements of a 2D vector using iterators, we need to use nested loops. The outer loop will iterate over the rows, while the inner loop will iterate over the columns.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Using nested loops and iterators to access elements
    for (auto rowIter = matrix.begin(); rowIter != matrix.end(); ++rowIter) {
        for (auto colIter = rowIter->begin(); colIter != rowIter->end(); ++colIter) {
            std::cout << *colIter << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

In the code above, we iterate over each row using the outer loop (`rowIter`) and for each row, we iterate over each column using the inner loop (`colIter`). We use `*colIter` to access and print the value of each element.

## Modifying Elements of a 2D Vector with Iterators

Iterators can also be used to modify elements of a 2D vector. We can access and modify elements in a similar way to the previous example.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Modifying elements of the 2D vector
    for (auto rowIter = matrix.begin(); rowIter != matrix.end(); ++rowIter) {
        for (auto colIter = rowIter->begin(); colIter != rowIter->end(); ++colIter) {
            *colIter += 1;
        }
    }

    // Printing the modified 2D vector
    for (auto row : matrix) {
        for (auto col : row) {
            std::cout << col << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

In the code above, we use `*colIter += 1` to increment each element of the 2D vector by 1. We then print the modified vector to verify the changes.

## Conclusion

Iterators are powerful tools for traversing and modifying elements of containers, such as 2D vectors. In this blog post, we discussed how to use iterators with 2D vectors and demonstrated examples of accessing and modifying elements with iterators. Using iterators can make working with 2D vectors more efficient and flexible. So go ahead and try using iterators when working with 2D vectors in your next project!

\#vectors #iterators