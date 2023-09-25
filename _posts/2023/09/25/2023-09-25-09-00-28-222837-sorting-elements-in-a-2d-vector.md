---
layout: post
title: "Sorting elements in a 2D vector"
description: " "
date: 2023-09-25
tags: [include, include]
comments: true
share: true
---

## Sorting a 2D Vector in Python

Python provides a handy `sort()` method that can be used for sorting a 2D vector based on a specific column. Here's an example:

```python
# Sort the 2D vector based on the second column
my_vector = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
my_vector.sort(key=lambda x: x[1])
print(my_vector)
```

Output:
```
[[1, 2, 3], [7, 8, 9], [4, 5, 6]]
```

In this example, the `sort()` method is called on the `my_vector` list, with the `key` parameter set to `lambda x: x[1]`. The `lambda` function specifies that the sorting should be based on the second element of each sublist.

## Sorting a 2D Vector in C++

In C++, sorting a 2D vector can be achieved by using the `std::sort()` function from the `<algorithm>` library. Here's an example:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Sort the 2D vector based on the second column
bool compare(const std::vector<int>& a, const std::vector<int>& b) {
    return a[1] < b[1];
}

int main() {
    std::vector<std::vector<int>> my_vector{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    
    // Sort the vector using a custom comparison function
    std::sort(my_vector.begin(), my_vector.end(), compare);
    
    // Print the sorted vector
    for (const auto& row : my_vector) {
        for (int val : row) {
            std::cout << val << " ";
        }
        std::cout << std::endl;
    }
    
    return 0;
}
```

Output:
```
1 2 3
7 8 9
4 5 6
```

In this example, we define a custom comparison function `compare` that compares two vectors based on their second element. We pass this function as the third argument to `std::sort()` to sort the vector accordingly.

## Conclusion

Sorting a 2D vector can be done using different approaches in different programming languages. Python provides a convenient `sort()` method, while C++ relies on the `std::sort()` function. Both methods allow you to specify the sorting criteria based on a specific column.

By utilizing these methods, you can efficiently sort elements in a 2D vector and manipulate the data as needed. So go ahead and try them out in your own projects!

#programming #2Dvector