---
layout: post
title: "Using vector of vectors as a matrix"
description: " "
date: 2023-09-25
tags: [cplusplus]
comments: true
share: true
---

In many programming languages, matrices can be represented using a two-dimensional array. However, in C++, we can also use a vector of vectors to represent a matrix. This approach offers more flexibility, as the size of each row can vary.

Let's see how we can use a vector of vectors to represent a matrix, perform basic operations on it, and access its elements.

## Creating a Matrix

To create a matrix using a vector of vectors, we first need to initialize the outer vector with the desired number of rows, and each row vector with the desired number of columns. Here's an example of creating a 3x3 matrix:

```cpp
#include <vector>

int main() {
    // Create a 3x3 matrix
    std::vector<std::vector<int>> matrix(3, std::vector<int>(3));

    // Accessing individual elements
    matrix[0][0] = 1;
    matrix[0][1] = 2;
    matrix[0][2] = 3;
    // ...

    return 0;
}
```

In this example, we create a `std::vector` called `matrix` with 3 elements, each initialized as a vector of 3 integers. This creates a 3x3 matrix where all elements are initialized to 0.

## Accessing Elements

We can access individual elements of the matrix using the square bracket notation. The first index signifies the row number, and the second index signifies the column number. For example:

```cpp
int element = matrix[1][2]; // Accessing the element at row 1, column 2
```

## Performing Operations

Since we are using a vector of vectors to represent a matrix, we can perform various operations on it, such as addition, subtraction, and multiplication (if the dimensions are compatible).

To perform these operations, we simply need to loop through the matrices and apply the corresponding operations to each element.

```cpp
{% raw %}
std::vector<std::vector<int>> matrix1 = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
std::vector<std::vector<int>> matrix2 = {{9, 8, 7}, {6, 5, 4}, {3, 2, 1}};
std::vector<std::vector<int>> result(3, std::vector<int>(3));

for (int i = 0; i < 3; ++i) {
    for (int j = 0; j < 3; ++j) {
        result[i][j] = matrix1[i][j] + matrix2[i][j]; // Perform addition
    }
}
{% endraw %}
```

## Conclusion

Using a vector of vectors as a matrix in C++ provides flexibility in terms of varying row sizes. It allows us to easily create, access, and perform operations on matrices. However, it's important to note that vector of vectors might not be the most efficient representation for large matrices due to the overhead of memory allocations.

#cplusplus #vectors #matrices