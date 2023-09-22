---
layout: post
title: "Recursive templates for searching algorithms in C++"
description: " "
date: 2023-09-22
tags: [include]
comments: true
share: true
---

Searching algorithms are an essential part of any programming language, allowing us to find specific elements in a collection of data efficiently. In this blog post, we will explore how recursive templates can be used to implement searching algorithms in C++.

## Binary Search Algorithm

Binary search is a commonly used searching algorithm that works efficiently on sorted arrays. It follows a divide and conquer approach to find the target element by repeatedly dividing the search range in half.

Let's start by defining a recursive template function for the binary search algorithm in C++:

```cpp
template <typename T>
int binarySearch(const std::vector<T>& arr, const T& target, int low, int high) {
    if (low > high) {
        return -1; // Element not found
    }

    int mid = low + (high - low) / 2;

    if (arr[mid] == target) {
        return mid; // Element found at index mid
    } else if (arr[mid] > target) {
        return binarySearch(arr, target, low, mid - 1); // Search left half
    } else {
        return binarySearch(arr, target, mid + 1, high); // Search right half
    }
}
```

In this template function, we use the `typename` keyword to indicate a template type. The function takes a vector `arr` containing elements of type `T`, the `target` element to be searched, and the search range defined by `low` and `high` indices.

The function first checks if the search range is valid (low > high) and returns -1 if the element is not found. If the element is found at the middle index (`arr[mid] == target`), the function returns the index. Otherwise, it recursively calls itself with updated search ranges based on the comparison of the middle element and the target element.

## Example Usage

Let's see an example of how to use the binary search template function:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15};
    int target = 9;

    int index = binarySearch(arr, target, 0, arr.size() - 1);

    if (index != -1) {
        std::cout << "Element " << target << " found at index " << index << std::endl;
    } else {
        std::cout << "Element " << target << " not found in the array" << std::endl;
    }

    return 0;
}
```

In this example, we define a sorted vector `arr` and a target value of 9. We call the `binarySearch` function with the initial search range of 0 to `arr.size() - 1`. If the element is found, we print the index; otherwise, we print a message indicating that the element was not found.

## Conclusion

Recursive templates provide a flexible and concise way to implement searching algorithms in C++. The binary search algorithm is a great example demonstrating the use of recursive templates to find elements efficiently in sorted arrays. Understanding and implementing these recursive templates can greatly enhance your searching algorithms and code efficiency.

#programming #C++