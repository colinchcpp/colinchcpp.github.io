---
layout: post
title: "Finding the sum of all elements in a 2D vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

## The Problem
Given a 2D vector, we want to calculate the sum of all its elements.

## The Solution
To find the sum of all elements in a 2D vector, we can use nested loops to iterate over each row and column. Here is a code snippet in C++ that demonstrates the approach:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int totalSum = 0;

    for (const auto& row : matrix) {
        for (const auto& element : row) {
            totalSum += element;
        }
    }

    std::cout << "Sum of all elements: " << totalSum << std::endl;

    return 0;
}
```

In this code, we initialize a 2D vector called `matrix` with some sample values. We then define a variable `totalSum` to track the sum of all elements. We use nested range-based for loops to iterate over each row and then each element within the row. We add each element to the `totalSum` variable.

Finally, we print out the calculated sum using `std::cout`.

## Conclusion
By using nested loops, we can easily calculate the sum of all elements in a 2D vector. This approach can be applied to any programming language that supports nested loops and supports 2D vector data structures.

Remember to adapt the code to the specific programming language you are using. Happy coding!

#programming #2Dvector #arrays #summation