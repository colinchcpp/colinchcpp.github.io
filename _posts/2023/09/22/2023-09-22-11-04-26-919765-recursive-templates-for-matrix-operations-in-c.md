---
layout: post
title: "Recursive templates for matrix operations in C++"
description: " "
date: 2023-09-22
tags: [matrix, recursive]
comments: true
share: true
---

Matrix operations are fundamental in many areas of computer science and data analysis. One efficient way to implement matrix operations is by using recursive templates in C++. Recursive templates allow us to handle matrices of varying dimensions without sacrificing performance. In this article, we will explore how to implement recursive templates for common matrix operations such as addition, multiplication, and transposition.

## Adding Matrices

To begin, let's define a `Matrix` class that will hold the data and dimensions of a matrix. We will also define a recursive template function `add` for adding two matrices.

```cpp
template <size_t Rows, size_t Cols>
struct Matrix {
    std::array<std::array<double, Cols>, Rows> data;
};

template <size_t Rows, size_t Cols, size_t Index = 0>
void add(const Matrix<Rows, Cols>& A, const Matrix<Rows, Cols>& B, Matrix<Rows, Cols>& result) {
    for (size_t i = 0; i < Cols; ++i) {
        result.data[Index][i] = A.data[Index][i] + B.data[Index][i];
    }

    if constexpr (Index + 1 < Rows) {
        add<Rows, Cols, Index + 1>(A, B, result);
    }
}
```

In the above code snippet, we use a recursive template function `add` to add corresponding elements of matrices A and B and store the result in the `result` matrix. The `if constexpr` statement ensures that the recursion terminates when `Index` reaches the number of rows.

## Multiplying Matrices

Next, let's implement a recursive template function `multiply` for multiplying two matrices.

```cpp
template <size_t Rows, size_t Cols, size_t K, size_t IndexI = 0, size_t IndexJ = 0>
void multiply(const Matrix<Rows, K>& A, const Matrix<K, Cols>& B, Matrix<Rows, Cols>& result) {
    if constexpr (IndexJ == Cols) {
        IndexI++;
        IndexJ = 0;
    }

    if constexpr (IndexI == Rows) {
        return;
    }

    double sum = 0;
    for (size_t k = 0; k < K; ++k) {
        sum += A.data[IndexI][k] * B.data[k][IndexJ];
    }
    result.data[IndexI][IndexJ] = sum;

    multiply<Rows, Cols, K, IndexI, IndexJ + 1>(A, B, result);
}
```

In the code snippet above, the `multiply` function multiplies matrices A and B by calculating the dot product of each row of A with each column of B, and stores the result in the `result` matrix. The recursion is controlled by `IndexI` and `IndexJ`, which increment until the multiplication is complete.

## Transposing a Matrix

Lastly, let's implement a recursive template function `transpose` to transpose a matrix.

```cpp
template <size_t Rows, size_t Cols, size_t Index = 0>
void transpose(const Matrix<Rows, Cols>& input, Matrix<Cols, Rows>& output) {
    for (size_t i = 0; i < Rows; ++i) {
        output.data[Index][i] = input.data[i][Index];
    }

    if constexpr (Index + 1 < Cols) {
        transpose<Rows, Cols, Index + 1>(input, output);
    }
}
```

The `transpose` function swaps the rows and columns of the input matrix and stores the result in the `output` matrix. The recursion continues until `Index` reaches the number of columns.

## Conclusion

Recursive templates provide a flexible and efficient way to perform matrix operations in C++. They allow us to handle matrices of arbitrary dimensions without sacrificing performance. By implementing recursive template functions for matrix addition, multiplication, and transposition, we have demonstrated the power and elegance of this technique.

#matrix #recursive-templates