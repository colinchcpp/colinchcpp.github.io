---
layout: post
title: "Finding the minimum and maximum values in a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

When working with a 2D vector or matrix, it is often necessary to find the minimum and maximum values within the dataset. In this blog post, we will explore how to efficiently find these values in a 2D vector using C++.

## Approach using Iteration

One straightforward approach to find the minimum and maximum values in a 2D vector is to iterate through all the elements and keep track of the minimum and maximum values found so far.

```cpp
#include <iostream>
#include <vector>

int main() {
    // Example 2D vector
    std::vector<std::vector<int>> matrix = {
        {5, 10, 3},
        {2, 8, 12},
        {4, 6, 1}
    };

    int minVal = matrix[0][0];
    int maxVal = matrix[0][0];

    for (const auto& row : matrix) {
        for (int val : row) {
            if (val < minVal) {
                minVal = val;
            }
            if (val > maxVal) {
                maxVal = val;
            }
        }
    }

    std::cout << "Minimum value: " << minVal << std::endl;
    std::cout << "Maximum value: " << maxVal << std::endl;

    return 0;
}
```

By initializing `minVal` and `maxVal` to the initial value of the first element in the vector, we can iterate through the entire vector and update these values accordingly. Finally, we print out the minimum and maximum values.

## Complexity Analysis

The time complexity of this approach is O(n*m), where n is the number of rows and m is the number of columns in the 2D vector. Since we need to iterate through all the elements once, the time complexity is directly proportional to the number of elements in the vector.

## Conclusion

Finding the minimum and maximum values in a 2D vector can be efficiently accomplished by iterating through all the elements and keeping track of the minimum and maximum values. This approach provides a straightforward solution to this problem.

#tech #programming