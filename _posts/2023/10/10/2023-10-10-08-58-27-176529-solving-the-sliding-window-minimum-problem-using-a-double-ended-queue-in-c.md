---
layout: post
title: "Solving the sliding window minimum problem using a double-ended queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will discuss the sliding window minimum problem and demonstrate how to solve it efficiently using a double-ended queue (deque) data structure in C++.

## Introduction

The sliding window minimum problem involves finding the minimum element in a fixed-size window as it slides through an array of integers. This problem can be solved using various approaches, but using a double-ended queue allows us to achieve an optimal time complexity of O(n).

## Approach

To solve the sliding window minimum problem using a double-ended queue, we can follow these steps:

1. Create an empty deque to store indices of elements.
2. Iterate through the array from left to right and perform the following steps for each element:
   - Remove any indices from the front of the deque that are no longer within the window size.
   - While the deque is not empty and the current element is smaller than or equal to the element at the back of the deque, remove the index from the back of the deque.
   - Add the current element's index to the back of the deque.
   - If the current index is greater than or equal to the window size minus one, add the element at the front of the deque to the result array.
3. Return the result array.

## Implementation

Here is the C++ implementation of the sliding window minimum algorithm using a double-ended queue:

```cpp
#include <iostream>
#include <deque>
#include <vector>

std::vector<int> slidingWindowMinimum(const std::vector<int>& nums, int k) {
    std::deque<int> dq;
    std::vector<int> result;
    
    for (int i = 0; i < nums.size(); i++) {
        // Remove indices from the front that are out of window
        if (!dq.empty() && dq.front() == i - k)
            dq.pop_front();

        // Remove indices from the back while the current element is smaller or equal
        while (!dq.empty() && nums[dq.back()] >= nums[i])
            dq.pop_back();

        // Add the current element's index to the back
        dq.push_back(i);

        // Add the element from the front of the deque to the result if it's within the window
        if (i >= k - 1)
            result.push_back(nums[dq.front()]);
    }
    
    return result;
}

int main() {
    std::vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    
    std::vector<int> result = slidingWindowMinimum(nums, k);
    
    std::cout << "Sliding Window Minimum: ";
    for (int num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This implementation utilizes the deque container from the C++ Standard Library to efficiently handle inserting and removing elements from both ends in constant time.

## Conclusion

By using a double-ended queue, we can efficiently solve the sliding window minimum problem with a time complexity of O(n). This approach allows us to find the minimum element in a window as it slides through an array of integers. The provided C++ implementation demonstrates how to solve this problem using a deque container.