---
layout: post
title: "Finding an element in a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

```cpp
#include <iostream>
#include <vector>

// Function to find an element in a 2D vector
bool findElementIn2DVector(const std::vector<std::vector<int>>& vec2d, int target) {
    for (const auto& vec : vec2d) {
        for (int element : vec) {
            if (element == target) {
                return true; // Element found
            }
        }
    }
    return false; // Element not found
}

int main() {
    // Example usage
    std::vector<std::vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int target = 5;

    if (findElementIn2DVector(matrix, target)) {
        std::cout << "Element " << target << " is found in the 2D vector!" << std::endl;
    } else {
        std::cout << "Element " << target << " is not found in the 2D vector." << std::endl;
    }

    return 0;
}
```

In the code above, we define a function `findElementIn2DVector` that takes in a 2D vector (`vec2d`) and a target element (`target`). We iterate over each element in the 2D vector using nested loops and check if the current element matches the target. If a match is found, we return `true`. If the loops finish executing without finding a match, we return `false`.

In the provided `main` function, we create an example 2D vector called `matrix` and set a target value of `5`. We then call the `findElementIn2DVector` function and output a respective message based on its return value.

This simple approach allows you to search for an element in a 2D vector easily. You can modify the code to perform additional actions once an element is found, such as obtaining its coordinates.