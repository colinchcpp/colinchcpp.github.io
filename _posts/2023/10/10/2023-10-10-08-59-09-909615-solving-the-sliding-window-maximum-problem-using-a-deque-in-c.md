---
layout: post
title: "Solving the sliding window maximum problem using a deque in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

The sliding window maximum problem involves finding the maximum element in each sliding window of size `k` in an array of integers. One efficient way to solve this problem is by using a double-ended queue (deque) data structure.

## Overview

A deque is a versatile data structure that allows insertion and deletion at both ends in constant time. By using a deque, we can efficiently maintain the maximum element for each sliding window as we traverse through the array.

## Approach

Here's a step-by-step approach to solving the sliding window maximum problem using a deque:

1. Create an empty deque to store the indices of the elements in the current window.

2. Initialize an empty vector or list to store the maximum elements for each window.

3. Traverse through the array and perform the following steps for each element `arr[i]`:

   - Remove any indices from the deque that are outside the current window (`i-k+1 > deque.front()`).
   - Remove any indices from the deque that correspond to elements smaller than the current element (`arr[i] > arr[deque.back()]`).
   - Add the current index `i` to the back of the deque.
   - If the front index of the deque is at least `i-k+1`, add the maximum element in the current window (`arr[deque.front()]`) to the result vector.

4. Return the vector of maximum elements for each window.

## Code Implementation

Here's an example implementation of the sliding window maximum problem using a deque in C++:

```cpp
#include <iostream>
#include <vector>
#include <deque>

std::vector<int> slidingWindowMaximum(const std::vector<int>& arr, int k) {
    std::vector<int> result;
    std::deque<int> deque;
    
    for (int i = 0; i < arr.size(); i++) {
        // Remove indices from the deque that are outside the current window
        if (!deque.empty() && deque.front() <= i - k)
            deque.pop_front();
        
        // Remove indices from the deque that correspond to smaller elements
        while (!deque.empty() && arr[i] > arr[deque.back()])
            deque.pop_back();
        
        // Add the current index to the back of the deque
        deque.push_back(i);
        
        // Add the maximum element in the current window to the result vector
        if (i >= k - 1)
            result.push_back(arr[deque.front()]);
    }
    
    return result;
}

int main() {
    std::vector<int> arr = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;

    std::vector<int> result = slidingWindowMaximum(arr, k);

    std::cout << "Maximum elements for each window of size " << k << ":" << std::endl;
    for (int i : result)
        std::cout << i << " ";
    
    return 0;
}
```

## Conclusion

Using a deque data structure, we can efficiently solve the sliding window maximum problem and find the maximum element for each window of size `k`. This approach has a time complexity of O(n) since each element is pushed and popped from the deque at most once.