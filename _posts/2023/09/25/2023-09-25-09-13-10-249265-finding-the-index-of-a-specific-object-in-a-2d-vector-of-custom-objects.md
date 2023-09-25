---
layout: post
title: "Finding the index of a specific object in a 2D vector of custom objects"
description: " "
date: 2023-09-25
tags: [programming, vectors]
comments: true
share: true
---

Working with multi-dimensional vectors in programming can sometimes be challenging, especially when dealing with custom objects. In this blog post, we will explore how to find the index of a specific object within a 2D vector of custom objects in a simple and efficient manner.

### Background

Before diving into the solution, let's first define what a 2D vector is. A 2D vector, also known as a matrix, is a container that holds elements arranged in a rectangular grid format. Each element within the matrix can be accessed using its row and column indices.

### The Problem

Let's assume we have a 2D vector called `matrix` that contains custom objects of type `MyObject`. Our task is to find the index (row and column) of a specific `MyObject` within this matrix.

### The Solution

To find the index of a specific object within a 2D vector, we need to iterate over each row and column of the vector until we find a match.

```cpp
int findIndexOfObject(const std::vector<std::vector<MyObject>>& matrix, const MyObject& targetObject) {
    for (int row = 0; row < matrix.size(); ++row) {
        for (int col = 0; col < matrix[row].size(); ++col) {
            if (matrix[row][col] == targetObject) {
                return row * matrix[row].size() + col;
            }
        }
    }
    return -1; // Return -1 if the object is not found in the matrix
}
```

In the code snippet above, we define a function called `findIndexOfObject` that takes in the 2D vector `matrix` and the `targetObject` we are looking for. We iterate over each row and column using nested for loops, comparing each object with the `targetObject`. If a match is found, we calculate the linear index of the element using the formula `row * matrix[row].size() + col`. Finally, we return the index if a match is found or -1 if the object is not present in the matrix.

### Usage Example

Let's see how we can use the `findIndexOfObject` function to locate the index of a specific object within a 2D vector.

```cpp
int main() {
    std::vector<std::vector<MyObject>> matrix = {
        {MyObject(1), MyObject(2), MyObject(3)},
        {MyObject(4), MyObject(5), MyObject(6)},
        {MyObject(7), MyObject(8), MyObject(9)},
    };

    MyObject target(5);
    int index = findIndexOfObject(matrix, target);

    if (index != -1) {
        std::cout << "The object is found at index " << index << std::endl;
    } else {
        std::cout << "Object not found in the matrix" << std::endl;
    }

    return 0;
}
```

In this example, we create a 2D vector `matrix` with custom objects, and we want to find the index of an object with value 5. After calling the `findIndexOfObject` function, we check if the returned index is -1 (indicating no match) or otherwise print the index.

### Conclusion

Finding the index of a specific object within a 2D vector of custom objects can be achieved by iterating over each element until a match is found. By using the provided code snippet, you can easily locate the index and perform further operations on the desired object within the matrix. #programming #vectors