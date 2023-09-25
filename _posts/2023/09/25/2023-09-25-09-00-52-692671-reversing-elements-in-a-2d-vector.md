---
layout: post
title: "Reversing elements in a 2D vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Reversing the elements in a 2D vector can be useful in various scenarios where you need to change the order of the data. In this blog post, we will explore different approaches to reverse the elements in a 2D vector using C++.

## Method 1: Using the `reverse` function

The simplest way to reverse the elements in a 2D vector is by using the built-in `reverse` function provided by the C++ Standard Library. This function allows us to reverse a range of elements in a container. Here's an example of how you can use it:

```c++
{% raw %}
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::vector<int>> vec = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    for (auto& row : vec) {
        std::reverse(row.begin(), row.end());
    }

    for (const auto& row : vec) {
        for (const auto& element : row) {
            std::cout << element << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
{% endraw %}
```

In this code snippet, we have a 2D vector `vec` initialized with some values. We then iterate over each row of the vector using a range-based for loop and apply the `reverse` function from the `<algorithm>` header to reverse the elements in each row. Finally, we print the modified vector to verify the results.

## Method 2: Using a Custom Reversal Algorithm

If you want more control over the reversal process, you can also implement a custom reversal algorithm. Here's an example implementation:

```c++
{% raw %}
#include <iostream>
#include <vector>

template <typename T>
void reverseVector(std::vector<std::vector<T>>& vec) {
    for (auto& row : vec) {
        std::reverse(row.begin(), row.end());
    }
}

int main() {
    std::vector<std::vector<int>> vec = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    reverseVector(vec);

    for (const auto& row : vec) {
        for (const auto& element : row) {
            std::cout << element << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
{% endraw %}
```

In this code snippet, we define a templated function `reverseVector` that takes a 2D vector as a parameter and reverses the elements in each row using the `reverse` function. We then call this function on our vector in the `main` function and print the modified vector.

## Conclusion

Reversing elements in a 2D vector can be done easily using the `reverse` function from the C++ Standard Library. However, if you need more control over the reversal process, you can implement your own custom reversal algorithm. The choice of method depends on your specific requirements and preferences.

#programming #C++