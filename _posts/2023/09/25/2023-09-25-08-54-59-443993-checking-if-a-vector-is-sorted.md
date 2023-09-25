---
layout: post
title: "Checking if a vector is sorted"
description: " "
date: 2023-09-25
tags: [programming, sorting]
comments: true
share: true
---

## Approach 1: Iterative Comparison

One way to check if a vector is sorted is to iteratively compare each element with its adjacent element. If all the adjacent elements are in the desired order, then the vector is sorted. Here's an example implementation in Python:

```python
def is_sorted(vector):
    for i in range(len(vector) - 1):
        if vector[i] > vector[i + 1]:
            return False
    return True
```

In the above code, we iterate over the vector and compare each element with its adjacent element. If any comparison shows that the order is not as desired, we immediately return `False`. If the loop completes without any mismatches, we return `True`.

However, this approach has a time complexity of O(n), where n is the size of the vector. In the worst case, we may need to compare every element with every other element in the vector.

## Approach 2: Sorted Function

A more straightforward approach is to use the built-in `sorted()` function. We can compare the original vector with the sorted version of the vector. If they are the same, then the vector is already sorted. Here's how it can be implemented in Python:

```python
def is_sorted(vector):
    return vector == sorted(vector)
```

This approach has a time complexity of O(nlogn), where n is the size of the vector. The `sorted()` function uses a sorting algorithm like merge sort or heap sort, which requires O(nlogn) comparisons.

## Conclusion

In summary, there are multiple ways to check if a vector is sorted or not. The approach you choose depends on the specific requirements of your application, as well as considerations for time and space complexity. Iteratively comparing adjacent elements offers a linear time complexity, while using the `sorted()` function provides a simpler implementation at the cost of a slightly higher time complexity. 

#programming #sorting