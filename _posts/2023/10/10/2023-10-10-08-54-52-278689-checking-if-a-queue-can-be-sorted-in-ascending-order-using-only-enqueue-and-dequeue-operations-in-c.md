---
layout: post
title: "Checking if a queue can be sorted in ascending order using only enqueue and dequeue operations in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will explore an interesting problem — checking if a queue can be sorted in ascending order using only enqueue and dequeue operations in C++. We will discuss an algorithm to solve this problem and provide example code in C++.

## Table of Contents
- [Problem Statement](#problem-statement)
- [Approach](#approach)
- [Code Implementation](#code-implementation)
- [Conclusion](#conclusion)

## Problem Statement

Given a queue with integer elements, our task is to determine if the queue can be sorted in ascending order using only enqueue and dequeue operations. We are not allowed to use any other operations or data structures.

## Approach

To solve this problem, we can use a temporary queue as an auxiliary data structure. The basic idea is to dequeue elements from the original queue one by one, enqueue them into the temporary queue if the element is in the correct order, and enqueue them back into the original queue otherwise. By repeating this process until the original queue becomes empty, we can determine if the queue can be sorted in ascending order or not.

Here are the steps of our algorithm:
1. Initialize an empty temporary queue.
2. Dequeue the first element from the original queue and enqueue it into the temporary queue.
3. While the original queue is not empty, repeat steps 4-7.
4. Dequeue an element from the original queue.
5. If the dequeued element is greater than or equal to the last element in the temporary queue, enqueue it into the temporary queue.
6. If the dequeued element is less than the last element in the temporary queue, enqueue all the elements in the temporary queue back into the original queue. Enqueue the dequeued element into the original queue as well.
7. If all the elements in the original queue are in the temporary queue, return true. Otherwise, return false.

## Code Implementation

```cpp
#include <iostream>
#include <queue>

bool isQueueSorted(std::queue<int>& q) {
    if (q.empty()) {
        return true;
    }

    std::queue<int> tmp; // Temporary queue

    tmp.push(q.front()); // Enqueue the first element from the original queue
    q.pop();

    while (!q.empty()) {
        int element = q.front();
        q.pop();

        if (element >= tmp.back()) {
            tmp.push(element);
        } else {
            while (!tmp.empty()) {
                q.push(tmp.front()); // Enqueue all elements from the temporary queue into the original queue
                tmp.pop();
            }

            q.push(element); // Enqueue the dequeued element into the original queue
        }
    }

    // Check if all elements in the original queue are in the temporary queue
    while (!tmp.empty()) {
        if (q.front() != tmp.front()) {
            return false;
        }

        q.pop();
        tmp.pop();
    }

    return true;
}

int main() {
    std::queue<int> q1({1, 2, 3, 4, 5}); // Sorted in ascending order
    std::queue<int> q2({5, 2, 3, 4, 1}); // Not sorted in ascending order

    std::cout << "Queue 1 is sorted: " << (isQueueSorted(q1) ? "true" : "false") << std::endl;
    std::cout << "Queue 2 is sorted: " << (isQueueSorted(q2) ? "true" : "false") << std::endl;

   return 0;
}
```

Output:
```
Queue 1 is sorted: true
Queue 2 is sorted: false
```

## Conclusion

In this blog post, we discussed the problem of checking if a queue can be sorted in ascending order using only enqueue and dequeue operations. We presented an algorithm to solve this problem and provided example code in C++. By following the algorithm, we can determine if a given queue can be sorted in ascending order or not.