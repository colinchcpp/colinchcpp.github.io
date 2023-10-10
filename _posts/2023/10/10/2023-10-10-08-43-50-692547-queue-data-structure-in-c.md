---
layout: post
title: "Queue data structure in C++"
description: " "
date: 2023-10-10
tags: [programming, datastructure]
comments: true
share: true
---

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. Elements are inserted at the back(rear) and deleted from the front. In this blog post, we'll explore how to implement a queue data structure in C++.

## Table of Contents
- [Introduction to Queue](#introduction-to-queue)
- [Implementing Queue in C++](#implementing-queue-in-c++)
- [Queue Operations](#queue-operations)
- [Conclusion](#conclusion)

## Introduction to Queue

A queue is similar to a real-life queue, such as people waiting in line for their turn. The element which is inserted first is the first one to be removed. It follows the FIFO (First-In-First-Out) order and provides operations like enqueue and dequeue.

## Implementing Queue in C++

```cpp
#include <iostream>
#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int front;
    int rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear == MAX_SIZE - 1);
    }

    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue." << std::endl;
            return;
        } else if (isEmpty()) {
            front = 0; // Set front to 0 when enqueueing the first element
        }
        arr[++rear] = value;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        } else if (front == rear) {
            // Reset front and rear to -1 when dequeueing the last element
            front = -1;
            rear = -1;
        } else {
            front++;
        }
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        std::cout << "Queue: ";
        for (int i = front; i <= rear; i++) {
            std::cout << arr[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue queue;
    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    queue.enqueue(40);
    queue.dequeue();
    queue.display();

    return 0;
}
```

## Queue Operations

The implemented queue data structure supports the following operations:

1. `enqueue(value)`: Inserts the given value at the rear end of the queue.
2. `dequeue()`: Removes the element from the front of the queue.
3. `isEmpty()`: Returns true if the queue is empty, and false otherwise.
4. `isFull()`: Returns true if the queue is full, and false otherwise.
5. `display()`: Prints the elements of the queue.

## Conclusion

Implementing a queue data structure in C++ is straightforward and can be useful in various scenarios. By understanding the operations and how they work together, you can effectively use queues in your programs for efficient data processing.

#programming #datastructure