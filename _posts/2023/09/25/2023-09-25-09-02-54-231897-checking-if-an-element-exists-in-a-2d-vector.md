---
layout: post
title: "Checking if an element exists in a 2D vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

```cpp
std::vector<std::vector<int>> matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
int target = 5;
bool elementExists = false;
```

To check if the `target` element exists in the `matrix`, we can iterate over each row and column using nested loops and compare each element with the `target`.

```cpp
for (int i = 0; i < matrix.size(); i++) {
    for (int j = 0; j < matrix[i].size(); j++) {
        if (matrix[i][j] == target) {
            elementExists = true;
            break;
        }
    }
    if (elementExists) {
        break;
    }
}
```

Here, we use a boolean variable `elementExists` to keep track of whether the element has been found or not. If the element is found, we set `elementExists` to `true` and break out of both loops.

Finally, we can check the value of `elementExists` to determine if the element exists in the 2D vector.

```cpp
if (elementExists) {
    std::cout << "Element exists in the vector." << std::endl;
} else {
    std::cout << "Element does not exist in the vector." << std::endl;
}
```

By using this approach, we can easily check if an element exists in a 2D vector.