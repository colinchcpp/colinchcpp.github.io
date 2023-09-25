---
layout: post
title: "Swapping elements in a 2D vector"
description: " "
date: 2023-09-25
tags: [cplusplus, 2Dvector]
comments: true
share: true
---

In this blog post, we will explore how to swap elements in a 2D vector using C++. A 2D vector is essentially a vector of vectors, representing a 2D grid or matrix. Swapping elements can be useful when reordering or manipulating data in the grid structure.

## Problem Statement

Let's say we have a 2D vector called `grid` that represents a 3x3 grid:

```cpp
vector<vector<int>> grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

Our task is to swap two elements in this grid. For example, let's swap the element at `grid[0][1]` (which is `2`) with the element at `grid[2][2]` (which is `9`).

## Solution

To swap elements in a 2D vector, we can follow these steps:

1. Store the value of the first element to be swapped in a temporary variable.
2. Assign the value of the second element to the first element.
3. Assign the value of the temporary variable to the second element.

Let's see how this can be implemented using the `grid` vector mentioned earlier:

```cpp
int tmp = grid[0][1];          // Step 1
grid[0][1] = grid[2][2];       // Step 2
grid[2][2] = tmp;              // Step 3
```

After executing these steps, the elements at `grid[0][1]` and `grid[2][2]` will be swapped, resulting in the following grid:

```cpp
{
    {1, 9, 3},
    {4, 5, 6},
    {7, 8, 2}
}
```

## Conclusion

Swapping elements in a 2D vector can be achieved by following these simple steps. It is a useful technique for reordering or manipulating data within the grid structure. By leveraging the power of `vector` in C++, we can easily perform such operations.

#cplusplus #2Dvector #SwapElements