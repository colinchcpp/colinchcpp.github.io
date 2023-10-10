---
layout: post
title: "Queue-based approach for printing a matrix in spiral form in C++"
description: " "
date: 2023-10-10
tags: [programming, algorithm]
comments: true
share: true
---

Printing a matrix in a spiral form is a common problem encountered in programming interviews or algorithmic challenges. In this blog post, we will explore a queue-based approach to solve this problem efficiently using C++.

## Problem Statement

Given a matrix with `n` rows and `m` columns, we need to print its elements in spiral order.

## Approach

The idea behind the queue-based approach is to use a queue to keep track of the elements of the matrix in the order they need to be printed. We will process the matrix layer by layer, starting from the outermost layer and moving towards the center.

Here are the steps to solve the problem:

1. Create an empty queue to store the elements.
2. Initialize two pointers `top`, `bottom` (denoting the top and bottom rows) and `left`, `right` (denoting the leftmost and rightmost columns) to the limits of the matrix.
3. Loop until `top <= bottom` and `left <= right`.
	1. Traverse the topmost row from left to right and enqueue each element in the queue.
	2. Traverse the rightmost column from top+1 to bottom and enqueue each element in the queue.
	3. Traverse the bottommost row from right-1 to left and enqueue each element in the queue.
	4. Traverse the leftmost column from bottom-1 to top+1 and enqueue each element in the queue.
	5. Update the pointers `top`, `bottom`, `left`, and `right` to move to the next layer of the matrix.
4. Print the elements of the queue, which will be the matrix elements in spiral order.

## Implementation

```cpp
#include <iostream>
#include <queue>
using namespace std;

void printMatrixInSpiral(vector<vector<int>>& matrix) {
    int n = matrix.size();
    int m = matrix[0].size();
    int top = 0, bottom = n - 1, left = 0, right = m - 1;

    queue<int> elements;
    
    while (top <= bottom && left <= right) {
        // Traverse the topmost row
        for (int i = left; i <= right; i++) {
            elements.push(matrix[top][i]);
        }
        top++;
        
        // Traverse the rightmost column
        for (int i = top; i <= bottom; i++) {
            elements.push(matrix[i][right]);
        }
        right--;
        
        // Traverse the bottommost row
        if (top <= bottom) {
            for (int i = right; i >= left; i--) {
                elements.push(matrix[bottom][i]);
            }
            bottom--;
        }
        
        // Traverse the leftmost column
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                elements.push(matrix[i][left]);
            }
            left++;
        }
    }
    
    // Print the elements in spiral order
    while (!elements.empty()) {
        cout << elements.front() << " ";
        elements.pop();
    }
}
```
## Sample Test Case

Let's test our implementation using the following matrix:

**Input:**
```
1 2 3
4 5 6
7 8 9
```

**Output:**
```
1 2 3 6 9 8 7 4 5
```

## Conclusion

In this blog post, we discussed a queue-based approach to print a matrix in spiral form using C++. This approach allows us to efficiently process the matrix layer by layer and maintain the correct order of the elements. By understanding and implementing this algorithm, we are better prepared to tackle similar problems in future coding challenges.

#programming #algorithm