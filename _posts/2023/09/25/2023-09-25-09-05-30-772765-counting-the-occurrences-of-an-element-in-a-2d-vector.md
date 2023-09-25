---
layout: post
title: "Counting the occurrences of an element in a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

When working with a 2D vector in programming, you may come across a situation where you need to count the occurrences of a specific element. In this blog post, we will explore how to accomplish this task using C++.

## Approach

We will iterate through each row of the 2D vector and then through each element in that row to check if it matches the target element. If a match is found, we will increment a counter variable.

## Example Code

Let's take a look at the following example code that demonstrates how to count the occurrences of an element in a 2D vector in C++:

```cpp
#include <iostream>
#include <vector>

// Function to count occurrences of an element in a 2D vector
int countOccurrences(const std::vector<std::vector<int>>& vec, int target) {
    int count = 0;
    for (const auto& row : vec) {
        for (const auto& element : row) {
            if (element == target) {
                count++;
            }
        }
    }
    return count;
}

int main() {
    std::vector<std::vector<int>> vec = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int target = 5;

    int occurrences = countOccurrences(vec, target);

    std::cout << "The element " << target << " occurs " << occurrences << " times." << std::endl;

    return 0;
}
```

In this code, we define a function `countOccurrences` that takes a 2D vector `vec` and a target element `target` as parameters. It initializes a counter `count` with a value of 0. We then use nested for-loops to iterate through each element in the 2D vector. If the current element matches the target element, we increment the `count` variable.

In the `main` function, we define a sample 2D vector `vec` and a target element `target` (in this case, 5). We then call the `countOccurrences` function to get the number of occurrences of the target element and print the result.

## Conclusion

Counting the occurrences of an element in a 2D vector can be easily achieved by iterating through each element and comparing it to the target element. In this blog post, we provided an example code in C++ that demonstrates how to implement this functionality. This approach can be extended or modified to suit your specific requirements.

#programming #C++