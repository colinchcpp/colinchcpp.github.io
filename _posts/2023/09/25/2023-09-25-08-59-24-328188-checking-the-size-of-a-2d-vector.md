---
layout: post
title: "Checking the size of a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

## Method 1: Using the `size()` function of the vector

In C++, vectors come with a handy `size()` function that returns the number of elements in the vector. To check the size of a 2D vector, we can simply call the `size()` function on the outer vector, which represents the number of rows. Additionally, we can access any inner vector to determine the number of columns since all the inner vectors are expected to have the same size.

Here's an example code snippet that demonstrates this approach:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::vector<int>> myVector = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int numRows = myVector.size();
    int numColumns = myVector[0].size();

    std::cout << "Number of rows: " << numRows << std::endl;
    std::cout << "Number of columns: " << numColumns << std::endl;

    return 0;
}
```

Running this code will output:

```
Number of rows: 3
Number of columns: 3
```

## Method 2: Using the `rows()` and `columns()` functions

If you prefer a more intuitive approach, you can create a class or a custom data structure to encapsulate the 2D vector and provide specialized member functions to access its size directly. For example, you can define `rows()` and `columns()` functions to get the number of rows and columns, respectively.

Here's an example code snippet demonstrating this approach:

```cpp
#include <iostream>
#include <vector>

class Matrix {
private:
    std::vector<std::vector<int>> data;

public:
    void addRow(std::vector<int> row) {
        data.push_back(row);
    }

    int rows() const {
        return data.size();
    }

    int columns() const {
        return data[0].size();
    }
};

int main() {
    Matrix myMatrix;
    
    myMatrix.addRow({1, 2, 3});
    myMatrix.addRow({4, 5, 6});
    myMatrix.addRow({7, 8, 9});

    std::cout << "Number of rows: " << myMatrix.rows() << std::endl;
    std::cout << "Number of columns: " << myMatrix.columns() << std::endl;

    return 0;
}
```

Running this code will produce the same output as before:

```
Number of rows: 3
Number of columns: 3
```

In conclusion, checking the size of a 2D vector is a common task when working with these data structures. By using either the `size()` function or by creating custom access functions, you can easily determine the number of rows and columns in a 2D vector, enabling you to perform various operations efficiently. #programming #C++