---
layout: post
title: "Removing duplicates from a 2D vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

## The Problem

Let's say you have a 2D vector containing integers:

```cpp
std::vector<std::vector<int>> matrix = {{1, 2, 3},
                                         {4, 5, 6},
                                         {1, 2, 3},
                                         {7, 8, 9}};
```

Your goal is to remove the duplicate sub-vectors from this matrix, resulting in the following unique elements:

```cpp
{{1, 2, 3},
 {4, 5, 6},
 {7, 8, 9}};
```

## The Solution

To remove duplicates from the 2D vector, we can use a hash set to keep track of the unique sub-vectors. We iterate over each sub-vector in the original matrix and check if it already exists in the hash set. If it doesn't, we add it to both the hash set and the resulting unique matrix.

Here's an example implementation in C++:

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <unordered_set>

std::vector<std::vector<int>> removeDuplicates(std::vector<std::vector<int>>& matrix) {
    std::unordered_set<std::vector<int>, std::hash<std::vector<int>>> uniqueSet;
    std::vector<std::vector<int>> uniqueMatrix;

    for (const auto& row : matrix) {
        if (uniqueSet.find(row) == uniqueSet.end()) {
            uniqueSet.insert(row);
            uniqueMatrix.push_back(row);
        }
    }

    return uniqueMatrix;
}

int main() {
    std::vector<std::vector<int>> matrix = {{1, 2, 3},
                                             {4, 5, 6},
                                             {1, 2, 3},
                                             {7, 8, 9}};

    std::vector<std::vector<int>> uniqueMatrix = removeDuplicates(matrix);

    for (const auto& row : uniqueMatrix) {
        for (int element : row) {
            std::cout << element << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
{% endraw %}
```

## Conclusion

By leveraging a hash set, we can efficiently remove duplicates from a 2D vector. This approach allows us to maintain the order of the original elements while producing a unique result. You can use this technique in your own projects to efficiently handle duplicate 2D vectors. #programming #duplicates