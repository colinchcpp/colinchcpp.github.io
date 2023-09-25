---
layout: post
title: "Introduction to C++ vectors"
description: " "
date: 2023-09-25
tags: [cplusplus]
comments: true
share: true
---

## What are C++ Vectors?

In C++, a vector is a sequence container that encapsulates dynamic arrays. Unlike static arrays, which have a fixed size, vectors can grow or shrink dynamically as elements are added or removed. This makes vectors a more flexible and convenient choice for storing collections of data.

## Creating a Vector

To use vectors in C++, you need to include the `<vector>` header file. Once included, you can create a vector using the following syntax:

```cpp
#include <vector>

// Create an empty vector
std::vector<int> numbers;

// Create a vector with initial values
std::vector<int> numbers = {1, 2, 3, 4, 5};
```

In the above example, we create two vectors: `numbers` and `numbers` with initial values. The angle brackets specify the type of elements the vector will store, in this case, `int`.

## Accessing and Modifying Elements

You can access elements in a vector using the indexing operator (`[]`) or the `at()` method. Here's an example:

```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};

// Access elements
int firstElement = numbers[0];
int secondElement = numbers.at(1);

// Modify elements
numbers[2] = 10;
```

In the above code snippet, we access and modify elements in the `numbers` vector. The first element is accessed using the indexing operator, the second element is accessed using the `at()` method, and the third element is modified using the indexing operator.

## Adding and Removing Elements

Adding elements to a vector is done using the `push_back()` method, while removing elements can be achieved using the `pop_back()` method or the `erase()` method. Here's an example:

```cpp
std::vector<int> numbers;

// Add elements
numbers.push_back(1);
numbers.push_back(2);
numbers.push_back(3);

// Remove elements
numbers.pop_back();
numbers.erase(numbers.begin() + 1);
```

In the above code snippet, we add elements to the `numbers` vector using the `push_back()` method. We then remove the last element using the `pop_back()` method and remove the second element using the `erase()` method.

## Conclusion

C++ vectors are a valuable tool for managing collections of data. They allow for dynamic resizing and provide convenient methods for accessing, modifying, adding, and removing elements. By incorporating vectors into your C++ programs, you can handle dynamic arrays with ease and efficiency.

#cplusplus #vectors