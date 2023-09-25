---
layout: post
title: "Checking if a 2D vector is sorted"
description: " "
date: 2023-09-25
tags: [python, sorting]
comments: true
share: true
---

When working with multidimensional data, it's common to come across situations where you need to determine if a 2D vector is sorted or not. This can be useful for various tasks, such as verifying if a matrix is in ascending or descending order.

In this blog post, we'll explore how to check if a 2D vector is sorted in either row-wise or column-wise order using Python. Let's get started!

## Checking if a vector is sorted row-wise

To check if a 2D vector is sorted row-wise, we can iterate over each row and compare each element with its adjacent element. If we find any element that is greater than the next one, the vector is not sorted.

Here's an example implementation in Python:

```python
def is_rowwise_sorted(matrix):
    for row in matrix:
        for i in range(len(row) - 1):
            if row[i] > row[i + 1]:
                return False
    return True
```

## Checking if a vector is sorted column-wise

To check if a 2D vector is sorted column-wise, we transpose the matrix (i.e., swap rows with columns) and apply the same logic as checking row-wise sorting.

Here's an example implementation:

```python
def is_columnwise_sorted(matrix):
    transposed_matrix = list(map(list, zip(*matrix)))  # Transpose the matrix
    return is_rowwise_sorted(transposed_matrix)
```

## Testing the functions

Let's test the functions with some examples:

```python
matrix_1 = [[1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]]

print(is_rowwise_sorted(matrix_1))  # Output: True
print(is_columnwise_sorted(matrix_1))  # Output: True

matrix_2 = [[1, 2, 3],
            [6, 5, 4],
            [7, 8, 9]]

print(is_rowwise_sorted(matrix_2))  # Output: False
print(is_columnwise_sorted(matrix_2))  # Output: False
```

As you can see, the functions correctly determine whether the given 2D vector is sorted row-wise or column-wise.

## Conclusion

In this blog post, we explored how to check if a 2D vector is sorted row-wise or column-wise using Python. By iterating through the rows or by transposing the matrix, we can compare each element with its adjacent element to determine its sorting order.

Remember to consider the cases where the vector may not be sorted in either order when using these functions. Also, keep in mind that the functions assume that the input is a valid 2D vector (a list of lists).

#python #sorting