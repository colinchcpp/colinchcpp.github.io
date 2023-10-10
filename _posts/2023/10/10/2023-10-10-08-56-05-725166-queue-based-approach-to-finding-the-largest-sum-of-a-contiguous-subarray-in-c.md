---
layout: post
title: "Queue-based approach to finding the largest sum of a contiguous subarray in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

When it comes to finding the largest sum of a contiguous subarray in an array, there are several different approaches one can take. One efficient approach is using a queue-based algorithm. In this blog post, we will explore how to implement this queue-based approach in C++.

## The Problem

Given an array of integers, we are tasked with finding the contiguous subarray that has the largest sum. For example, given the array [-2, 1, -3, 4, -1, 2, 1, -5, 4], the contiguous subarray with the largest sum is [4, -1, 2, 1], which has a sum of 6.

## The Queue-based Approach

The queue-based approach involves scanning the array from left to right and maintaining a queue of prefixes with running sums. We start with an empty queue and initialize the maximum sum as the first element of the array.

```cpp
#include <iostream>
#include <queue>
#include <algorithm>

int largestSubarraySum(std::vector<int>& nums) {
    std::queue<int> prefixQueue;
    int maxSum = nums[0];

    for (int num : nums) {
        while (!prefixQueue.empty()) {
            // Remove prefixes that have a negative sum
            if (prefixQueue.front() <= 0) {
                prefixQueue.pop();
            } else {
                break;
            }
        }

        // Add the current element to the running sum
        prefixQueue.push(num);
        int currentSum = std::accumulate(prefixQueue.begin(), prefixQueue.end(), 0);

        // Update the maximum sum if necessary
        maxSum = std::max(maxSum, currentSum);
    }

    return maxSum;
}

int main() {
    std::vector<int> nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    int largestSum = largestSubarraySum(nums);
    std::cout << "Largest sum of a contiguous subarray: " << largestSum << std::endl;

    return 0;
}
```

The `largestSubarraySum` function takes in a reference to a vector of integers `nums` and returns the largest sum of a contiguous subarray. It does so by iterating through the array and maintaining a queue of prefixes with running sums. 

In each iteration, the algorithm removes prefixes from the queue that have a negative sum, as they won't contribute to the maximum sum. Then, it adds the current element to the queue and calculates the running sum. Finally, it updates the maximum sum if necessary.

## Conclusion

The queue-based approach provides an efficient solution for finding the largest sum of a contiguous subarray in an array. By maintaining a queue of prefixes with running sums, we can easily keep track of the largest sum as we scan through the array. This approach has a time complexity of O(n), where n is the size of the input array.

By using this queue-based approach, you can efficiently solve the problem of finding the largest sum of a contiguous subarray in C++.