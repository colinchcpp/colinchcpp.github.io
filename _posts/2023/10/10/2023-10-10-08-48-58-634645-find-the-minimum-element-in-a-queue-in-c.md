---
layout: post
title: "Find the minimum element in a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

## Table of Contents
- [The Problem](#the-problem)
- [Approach](#approach)
- [Implementation in C++](#implementation-in-c)
- [Conclusion](#conclusion)

## The Problem
Given a queue of integers, we need to find the minimum element in the queue. The queue can be of any size, and it may contain duplicate elements.

## Approach
One approach to find the minimum element in a queue is to traverse the entire queue and keep track of the minimum element encountered so far. This can be done using a temporary variable that is initialized with the first element of the queue, and then updated if a smaller element is found during the traversal.

Another approach is to use an extra queue to store the elements temporarily. We can remove elements from the original queue one by one, compare them with the minimum element found so far, and store them in the extra queue if they are smaller. Finally, we can enqueue the elements from the extra queue back into the original queue.

The second approach has a better time complexity since the minimum element can be found in a single traversal, but it requires extra space to store the elements temporarily.

## Implementation in C++
Here is an implementation of the second approach in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

int findMinimumElement(queue<int>& q) {
    // Initialize a variable to store the minimum element
    int minimum = q.front();

    // Create an extra queue
    queue<int> tempQueue;

    // Traverse the original queue
    while (!q.empty()) {
        int current = q.front();

        // Check if the current element is smaller than the minimum
        if (current < minimum) {
            minimum = current;
        }

        // Move the element to the extra queue
        tempQueue.push(current);
        q.pop();
    }

    // Enqueue the elements back into the original queue
    while (!tempQueue.empty()) {
        q.push(tempQueue.front());
        tempQueue.pop();
    }

    return minimum;
}

int main() {
    queue<int> q;
    q.push(5);
    q.push(2);
    q.push(8);
    q.push(1);
    q.push(3);

    int minimum = findMinimumElement(q);
    cout << "Minimum element in the queue is: " << minimum << endl;

    return 0;
}
```

## Conclusion
Finding the minimum element in a queue can be achieved by using a temporary variable or by using an extra queue. The choice of approach depends on the specific requirements of your application, considering time complexity and space complexity. By implementing the second approach discussed in this blog post, you can efficiently find the minimum element in a queue using C++.