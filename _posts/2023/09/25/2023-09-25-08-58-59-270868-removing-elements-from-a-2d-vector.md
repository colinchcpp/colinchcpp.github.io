---
layout: post
title: "Removing elements from a 2D vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Removing elements from a 2D vector can be approached in several ways, depending on the specific requirements of your use case. Here, we will explore two common methods: using the `erase` function and using the `remove_if` algorithm.

## Method 1: Using the 'erase' function

If you are using C++, the `erase` function can be utilized to remove elements from a 2D vector. This method is ideal when you know the exact position of the element you want to remove.

```cpp
{% raw %}
#include <vector>

int main() {
    std::vector<std::vector<int>> myVector = {{1, 2, 3},
                                              {4, 5, 6},
                                              {7, 8, 9}
                                             };

    int rowToRemove = 1;
    myVector.erase(myVector.begin() + rowToRemove);

    return 0;
}
{% endraw %}
```

In this example, the second row (`rowToRemove = 1`) is removed using the `erase` function, which takes an iterator as an argument. To remove a specific column, you can use the `erase` function on individual rows.

## Method 2: Using the 'remove_if' algorithm

The `remove_if` algorithm in C++ is another powerful tool for removing elements based on a certain condition. This method is useful when you want to remove elements that meet specific criteria.

```cpp
{% raw %}
#include <vector>
#include <algorithm>

bool isEven(int num) {
    return num % 2 == 0;
}

int main() {
    std::vector<std::vector<int>> myVector = {{1, 2, 3},
                                              {4, 5, 6},
                                              {7, 8, 9}
                                             };

    int rowToRemove = 1;
    myVector[rowToRemove].erase(std::remove_if(myVector[rowToRemove].begin(), myVector[rowToRemove].end(), isEven), myVector[rowToRemove].end());

    return 0;
}
{% endraw %}
```

In this example, the `isEven` function is used as the condition to remove even numbers from the second row. The `remove_if` algorithm returns an iterator pointing to the new end of the vector, and then the `erase` function is used to delete the elements.

## Conclusion

Removing elements from a 2D vector can be achieved using various methods, depending on your requirements. Whether you prefer using the `erase` function or the `remove_if` algorithm, it's important to choose the method that best fits your use case.

#programming #tutorial