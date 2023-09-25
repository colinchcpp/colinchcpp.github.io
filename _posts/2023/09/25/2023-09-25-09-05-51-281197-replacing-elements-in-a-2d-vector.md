---
layout: post
title: "Replacing elements in a 2D vector"
description: " "
date: 2023-09-25
tags: [techblog, coding]
comments: true
share: true
---

In this blog post, we will explore how to replace elements in a 2D vector using various methods and techniques. We will cover two common scenarios: replacing a single element at a given position, and replacing multiple elements based on certain criteria.

### Scenario 1: Replacing a Single Element

To replace a single element in a 2D vector, we need to know the position of the element we want to replace. Let's say we have a 2D vector called `matrix` of size `m x n`, and we want to replace the element at position `(i, j)` with a new value `newVal`.

Here's an example in C++:

```cpp
vector<vector<int>> matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Replace element at position (1, 2) with a new value
int i = 1; // row index
int j = 2; // column index
int newVal = 10;

matrix[i][j] = newVal;
```

In this example, we have a 3x3 matrix and we want to replace the element at position (1, 2) with the value 10. By accessing the element using `matrix[i][j]`, we can assign a new value to it.

### Scenario 2: Replacing Multiple Elements

In some cases, we may want to replace multiple elements in a 2D vector based on certain criteria. For instance, let's say we have a 2D vector `matrix` of size `m x n`, and we want to replace all occurrences of a specific value `oldVal` with a new value `newVal`.

Here's an example in Python:

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

oldVal = 2
newVal = 20

for row in matrix:
    for i in range(len(row)):
        if row[i] == oldVal:
            row[i] = newVal
```

In this example, we have a 3x3 matrix and we want to replace all occurrences of the value 2 with the value 20. We iterate over each row, and for each element in the row, we check if it matches the `oldVal`. If it does, we replace it with the `newVal`.

### Conclusion

Replacing elements in a 2D vector can be done by accessing the specific position or by iterating over the vector and applying certain criteria. By understanding these techniques, you can easily replace elements in a 2D vector based on your needs.

#techblog #coding