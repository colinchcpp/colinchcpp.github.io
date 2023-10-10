---
layout: post
title: "Finding the maximum value of each sub-array of a given array using a queue in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

When working with arrays, it is often necessary to find the maximum value of each sub-array. One efficient way to tackle this problem is by using a queue data structure. In this tutorial, we will explore how to find the maximum value of each sub-array of a given array using a queue in C++.

## Table of Contents

1. [Introduction](#introduction)
2. [Approach](#approach)
3. [Implementation](#implementation)
4. [Example](#example)
5. [Conclusion](#conclusion)

## Introduction

The problem requires us to find the maximum value of each sub-array of a given array. A sub-array is a contiguous part of the array. We will use a queue to efficiently find the maximum value of each sub-array.

## Approach

1. Create an empty queue to store the elements of the sub-array.
2. Iterate through the given array.
3. For each element, check if the queue is empty.
4. If the queue is empty, simply push the current element into the queue.
5. If the queue is not empty, compare the current element with the last element of the queue.
6. If the current element is greater than the last element of the queue, remove all the elements from the queue and push the current element.
7. If the current element is less than or equal to the last element of the queue, simply push the current element.
8. Print the maximum element of the queue, which represents the maximum value of the current sub-array.
9. Repeat steps 3-8 until all sub-arrays have been processed.

## Implementation

Here is the C++ code that implements the above approach:

```C++
#include <iostream>
#include <queue>
using namespace std;

void findMaxSubArray(int arr[], int n, int k) {
    queue<int> q;
    int i;
    for (i = 0; i < k; i++) {
        while (!q.empty() && arr[i] >= arr[q.back()]) {
            q.pop();
        }
        q.push(i);
    }
    for (; i < n; i++) {
        cout << arr[q.front()] << " ";
        while (!q.empty() && q.front() <= i - k) {
            q.pop();
        }
        while (!q.empty() && arr[i] >= arr[q.back()]) {
            q.pop();
        }
        q.push(i);
    }
    cout << arr[q.front()] << endl;
}

int main() {
    int arr[] = {1, 3, -1, -3, 5, 3, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    findMaxSubArray(arr, n, k);
    return 0;
}
```

## Example

Let's take the example of the array `[1, 3, -1, -3, 5, 3, 6, 7]` and `k = 3` (the size of the sub-array).

The maximum value of each sub-array would be `[3, 3, 5, 5, 6, 7]`. The output of the above code will be:

```
3 3 5 5 6 7
```

## Conclusion

In this tutorial, we have learned how to find the maximum value of each sub-array of a given array using a queue data structure in C++. By implementing the approach discussed above, we can efficiently solve this problem in linear time complexity.

#programming #C++