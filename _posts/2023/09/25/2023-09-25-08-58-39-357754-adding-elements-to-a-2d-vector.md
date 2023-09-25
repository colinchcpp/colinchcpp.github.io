---
layout: post
title: "Adding elements to a 2D vector"
description: " "
date: 2023-09-25
tags: [2DVector]
comments: true
share: true
---

In C++, you can use a vector to store elements in a dynamically resizable array. A 2D vector is simply a vector of vectors, where each inner vector represents a row of elements.

To add elements to a 2D vector, you can follow these steps:

1. Declare the 2D vector:
```cpp
std::vector<std::vector<int>> matrix;
```

2. Add elements to the 2D vector:
```cpp
matrix.push_back({1, 2, 3});     // Adds a new row {1, 2, 3}
matrix.push_back({4, 5, 6});     // Adds a new row {4, 5, 6}
```

You can also add elements individually to a specific row:
```cpp
matrix[0].push_back(7);          // Adds 7 to the first row
matrix[1].push_back(8);          // Adds 8 to the second row
```

3. Accessing the elements in the 2D vector:
To access a specific element in the 2D vector, you need to specify the row and column index:
```cpp
int element = matrix[row_index][col_index];
```

4. Iterating over the 2D vector:
You can use nested loops to iterate over the elements of the 2D vector:
```cpp
for (size_t i = 0; i < matrix.size(); i++) {
    for (size_t j = 0; j < matrix[i].size(); j++) {
        // Access and process the elements
        int element = matrix[i][j];
    }
}
```

By following these steps, you can easily add elements to a 2D vector in C++. The flexibility of vectors allows you to dynamically resize and manipulate the 2D structure according to your needs.

#C++ #2DVector