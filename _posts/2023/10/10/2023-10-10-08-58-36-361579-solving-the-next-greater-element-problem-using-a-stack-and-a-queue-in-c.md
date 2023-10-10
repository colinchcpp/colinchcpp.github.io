---
layout: post
title: "Solving the next greater element problem using a stack and a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

## Introduction

The *Next Greater Element* problem is a common algorithmic problem in computer science. Given an array of integers, we need to find the next greater element for each element in the array. In other words, for each element, we need to find the first element to its right that is greater than the current element.

In this blog post, we will discuss an efficient approach to solve the Next Greater Element problem using a stack and a queue in C++.

## Algorithm

1. Create an empty stack and an empty queue.
2. Traverse the array from right to left.
3. For each element, do the following:
    * While the stack is not empty and the top element of the stack is smaller than or equal to the current element, keep popping elements from the stack.
    * If the stack becomes empty, insert -1 into the queue.
    * Otherwise, insert the top element of the stack into the queue.
    * Push the current element into the stack.
4. Reverse the queue.
5. Print the elements of the queue.

## Implementation

Here is the C++ implementation of the algorithm:

```cpp
#include <iostream>
#include <stack>
#include <queue>
using namespace std;

void nextGreaterElement(int arr[], int n) {
    stack<int> s;
    queue<int> q;
    for (int i = n - 1; i >= 0; i--) {
        while (!s.empty() && s.top() <= arr[i]) {
            s.pop();
        }
        if (s.empty()) {
            q.push(-1);
        } else {
            q.push(s.top());
        }
        s.push(arr[i]);
    }
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
}

int main() {
    int arr[] = { 3, 4, 2, 7, 5, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    nextGreaterElement(arr, n);
    return 0;
}
```

## Conclusion

In this blog post, we discussed an efficient approach to solving the Next Greater Element problem using a stack and a queue in C++. By using a stack to keep track of the previous elements and a queue to store the next greater elements, we can solve the problem in linear time complexity.

By following the algorithm and implementing the code provided, you should be able to solve the Next Greater Element problem in C++.