---
layout: post
title: "Copying a vector to another vector"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

## Copying a Vector in C++

In C++, you can copy the contents of one vector to another by using the assignment operator (=) or the `assign()` function. Here's an example:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> sourceVec = {1, 2, 3, 4, 5};
    std::vector<int> destVec;

    // Using the assignment operator
    destVec = sourceVec;

    // Using the assign() function
    // destVec.assign(sourceVec.begin(), sourceVec.end());

    // Print the contents of destVec
    for (int num : destVec) {
        std::cout << num << " ";
    }

    return 0;
}
```

In the above example, we have a source vector `sourceVec` with elements {1, 2, 3, 4, 5}. We then copy this vector to an empty destination vector `destVec` using the assignment operator (=). We can also use the `assign()` function to achieve the same result.

## Copying a Vector in Python

In Python, you can copy a vector (list) to another vector by using the `copy()` method or by using the `[:]` slicing technique. Here's an example:

```python
sourceVec = [1, 2, 3, 4, 5]
destVec = []

# Using the copy() method
destVec = sourceVec.copy()

# Using the [:] slicing technique
# destVec = sourceVec[:]

# Print the contents of destVec
for num in destVec:
    print(num, end=" ")
```

In the above example, we have a source vector `sourceVec` with elements [1, 2, 3, 4, 5]. We then copy this vector to an empty destination vector `destVec` using either the `copy()` method or the `[:]` slicing technique.

## Conclusion

Copying a vector to another vector is a common operation when working with collections of data. In this blog post, we explored different methods of performing this task in C++ and Python. Keep in mind that the choice of which method to use may depend on the specific requirements of your programming project.

#programming #vectors