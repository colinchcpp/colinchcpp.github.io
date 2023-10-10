---
layout: post
title: "Interleave the first half of a queue with the second half in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

<!-- TOC -->
- [Introduction](#introduction)
- [Problem Statement](#problem-statement)
- [Approach](#approach)
- [Code Implementation](#code-implementation)
- [Conclusion](#conclusion)
<!-- /TOC -->

## Introduction

In this blog post, we will discuss how to interleave the first half of a queue with the second half in C++. We will provide an approach to solve this problem and implement it using C++ code.

## Problem Statement

Given a queue containing a list of elements, we want to interleave the first half of the queue with the second half. The interleaved queue should have the first element from the first half, followed by the first element from the second half, and so on. If the queue has an odd number of elements, the middle element should remain at the same position.

For example, if the original queue is [1, 2, 3, 4, 5], the interleaved queue should be [1, 4, 2, 5, 3].

## Approach

To interleave the first half of the queue with the second half, we can use the following approach:

1. Calculate the size of the queue.
2. Create two temporary queues, `firstHalf` and `secondHalf`.
3. Push the elements of the original queue into `firstHalf` until reaching the middle element.
4. Push the remaining elements of the original queue into `secondHalf`.
5. Create a new result queue.
6. While either `firstHalf` or `secondHalf` is not empty, dequeue from `firstHalf` and enqueue into the result queue. Then, dequeue from `secondHalf` and enqueue into the result queue.
7. The result queue will be the interleaved queue.

## Code Implementation

```cpp
#include <iostream>
#include <queue>

std::queue<int> interleaveQueue(std::queue<int>& inputQueue) {
    std::queue<int> firstHalf, secondHalf, result;

    int size = inputQueue.size();
    int halfSize = size / 2;

    for (int i = 0; i < halfSize; i++) {
        firstHalf.push(inputQueue.front());
        inputQueue.pop();
    }

    while (!inputQueue.empty()) {
        secondHalf.push(inputQueue.front());
        inputQueue.pop();
    }

    while (!firstHalf.empty() || !secondHalf.empty()) {
        if (!firstHalf.empty()) {
            result.push(firstHalf.front());
            firstHalf.pop();
        }

        if (!secondHalf.empty()) {
            result.push(secondHalf.front());
            secondHalf.pop();
        }
    }

    return result;
}

int main() {
    std::queue<int> inputQueue;
    inputQueue.push(1);
    inputQueue.push(2);
    inputQueue.push(3);
    inputQueue.push(4);
    inputQueue.push(5);

    std::queue<int> interleavedQueue = interleaveQueue(inputQueue);

    while (!interleavedQueue.empty()) {
        std::cout << interleavedQueue.front() << " ";
        interleavedQueue.pop();
    }

    return 0;
}
```

## Conclusion

In this blog post, we discussed how to interleave the first half of a queue with the second half in C++. We provided an approach to solve this problem and implemented it using C++ code. Interleaving a queue can be a useful operation in scenarios where we need to maintain the ordering of elements while rearranging them.