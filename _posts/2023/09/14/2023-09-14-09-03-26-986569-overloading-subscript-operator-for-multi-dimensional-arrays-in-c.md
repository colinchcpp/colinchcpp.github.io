---
layout: post
title: "Overloading subscript operator for multi-dimensional arrays in C++"
description: " "
date: 2023-09-14
tags: [multidimensionalarray, operatoroverloading]
comments: true
share: true
---

In C++, the subscript operator `[]` allows us to access elements of arrays using index values. However, by default, it only works for one-dimensional arrays. To work with multi-dimensional arrays, we can overload the subscript operator, enabling us to access elements using multiple indices.

## Creating a Class to Represent Multi-Dimensional Arrays

To overload the subscript operator, we first need to create a class to represent our multi-dimensional array. Let's call this class `Array2D`. Here is an example implementation:

```cpp
class Array2D {
private:
    int** data; // pointer to the actual data
    int rows;   // number of rows
    int cols;   // number of columns

public:
    // Constructor
    Array2D(int numRows, int numCols) : rows(numRows), cols(numCols) {
        // Allocate memory for the array
        data = new int*[rows];
        for (int i = 0; i < rows; ++i) {
            data[i] = new int[cols];
        }
    }

    // Destructor
    ~Array2D() {
        // Deallocate memory
        for (int i = 0; i < rows; ++i) {
            delete[] data[i];
        }
        delete[] data;
    }

    // Overloaded subscript operator
    int& operator()(int row, int col) {
        return data[row][col];
    }
};
```

## Using the Overloaded Subscript Operator

Now that we have our `Array2D` class with the subscript operator overloaded, we can use it to access elements of multi-dimensional arrays. Here's an example usage:

```cpp
int main() {
    Array2D array(3, 3);

    // Assigning values to the array
    array(0, 0) = 1;
    array(0, 1) = 2;
    array(0, 2) = 3;
    array(1, 0) = 4;
    array(1, 1) = 5;
    array(1, 2) = 6;
    array(2, 0) = 7;
    array(2, 1) = 8;
    array(2, 2) = 9;

    // Accessing and printing array elements
    std::cout << "Value at (1, 1): " << array(1, 1) << std::endl;
    std::cout << "Value at (2, 0): " << array(2, 0) << std::endl;

    return 0;
}
```

In the above example, we create a `Array2D` object called `array` with 3 rows and 3 columns. We then assign values to the array using the overloaded subscript operator. Finally, we access array elements using the same operator and print them to the console.

With the subscript operator overloaded, working with multi-dimensional arrays becomes more convenient and intuitive in C++. However, it's important to handle memory allocation and deallocation properly to prevent memory leaks.

#cpp #multidimensionalarray #operatoroverloading