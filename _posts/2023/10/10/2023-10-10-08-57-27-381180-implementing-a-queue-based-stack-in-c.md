---
layout: post
title: "Implementing a queue-based stack in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

When working with data structures, it's common to encounter situations where you need to implement one data structure using another. In this article, we'll explore how to implement a stack data structure using queues in C++.

## What is a stack?

A stack is a data structure that follows the LIFO (Last-In, First-Out) principle. It allows two main operations: `push` (to add an element to the top of the stack) and `pop` (to remove the top element from the stack).

## What is a queue?

A queue is another data structure that follows the FIFO (First-In, First-Out) principle. Elements are added to the end of the queue, and removed from the front.

## The Queue-Based Stack Implementation

To implement a stack using queues, we can utilize two queues, let's call them `q1` and `q2`. The `q1` queue will be used to store the elements of the stack, while `q2` will be used for temporary storage during certain operations.

### Algorithm

1. Implement the `push` operation:
   - Enqueue the new element into `q1`.
   
2. Implement the `pop` operation:
   - If `q1` is empty, throw an exception or return an error message.
   - Dequeue all elements from `q1` except the last one, and enqueue them into `q2`.
   - Dequeue the last element from `q1` and return it as the popped value.
   - Swap `q1` and `q2` (i.e., make `q2` the new `q1`).

### Code Implementation

```cpp
#include <queue>
#include <exception>

class QueueStack {
    std::queue<int> q1, q2;

public:
    void push(int value) {
        q1.push(value);
    }

    int pop() {
        if (q1.empty()) {
            throw std::runtime_error("Stack is empty");
        }

        // Move elements from q1 to q2, except the last one
        while (q1.size() > 1) {
            q2.push(q1.front());
            q1.pop();
        }

        // Get the last element in q1
        int poppedValue = q1.front();
        q1.pop();

        // Swap q1 and q2
        std::swap(q1, q2);

        return poppedValue;
    }
};
```

### Usage

```cpp
#include <iostream>

int main() {
    QueueStack stack;

    // Pushing elements into the stack
    stack.push(1);
    stack.push(2);
    stack.push(3);

    // Popping elements from the stack
    std::cout << stack.pop() << std::endl;  // Output: 3
    std::cout << stack.pop() << std::endl;  // Output: 2
    std::cout << stack.pop() << std::endl;  // Output: 1

    return 0;
}
```

## Conclusion

In this article, we learned about implementing a stack data structure using queues in C++. By utilizing two queues and the enqueue and dequeue operations, we were able to achieve the stack functionality. We also provided a code implementation and a usage example for better understanding.