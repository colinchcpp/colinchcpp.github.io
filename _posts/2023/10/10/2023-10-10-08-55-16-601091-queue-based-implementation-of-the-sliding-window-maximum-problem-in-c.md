---
layout: post
title: "Queue-based implementation of the sliding window maximum problem in C++"
description: " "
date: 2023-10-10
tags: [slidingwindow]
comments: true
share: true
---

The sliding window maximum problem involves finding the maximum element in a window of fixed size as it slides through an array or a sequence. In this article, we will explore a queue-based approach to solve this problem in C++.

## Introduction to the Sliding Window Maximum Problem

Given an array `arr` of integers and a window size `k`, we need to find the maximum element in each window of size `k` as it slides through the array. For example, consider the array `[1, 3, -1, -3, 5, 3, 6, 7]` and a window size of `3`. The expected output would be `[3, 3, 5, 5, 6, 7]`, which represents the maximum element in each window.

## Approach

To solve this problem, we will use a queue data structure. The idea is to maintain a sliding window of maximum elements. At each step, we will enqueue the current element into the queue and dequeue elements from the front until we find an element greater than the current element. This ensures that the front of the queue always contains the maximum element of the current window.

## Implementation

Let's implement the queue-based solution in C++.

```c++
#include <iostream>
#include <deque>
#include <vector>

std::vector<int> slidingWindowMaximum(std::vector<int>& arr, int k) {
    std::vector<int> result;
    std::deque<int> window;
    
    for (int i = 0; i < arr.size(); i++) {
        // Remove elements from the front smaller than the current element
        while (!window.empty() && arr[i] >= arr[window.back()]) {
            window.pop_back();
        }
        
        // Remove elements outside the current window range
        while (!window.empty() && window.front() <= i - k) {
            window.pop_front();
        }
        
        // Push the current element to the window
        window.push_back(i);
        
        // Add the maximum element to the result
        if (i >= k - 1) {
            result.push_back(arr[window.front()]);
        }
    }
    
    return result;
}

int main() {
    std::vector<int> arr = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    
    std::vector<int> result = slidingWindowMaximum(arr, k);
    
    // Print the result
    for (int i = 0; i < result.size(); i++) {
        std::cout << result[i] << " ";
    }
    
    return 0;
}
```

## Complexity Analysis

The time complexity of this approach is O(n) since we process each element in the array exactly once. The space complexity is O(k) because we store a maximum of `k` elements in the queue.

## Conclusion

In this article, we have implemented a queue-based solution to the sliding window maximum problem in C++. We utilized a deque for efficient insertion and removal of elements from both ends. This approach allows us to find the maximum element in each window of a fixed size efficiently.

#Hashtags: #cpp #slidingwindow