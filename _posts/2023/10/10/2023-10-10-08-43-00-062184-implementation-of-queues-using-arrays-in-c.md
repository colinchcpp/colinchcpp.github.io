---
layout: post
title: "Implementation of queues using arrays in C++"
description: " "
date: 2023-10-10
tags: [queues, datastructures]
comments: true
share: true
---

Queues are a fundamental data structure in computer science that follow the First-In-First-Out (FIFO) principle. In this blog post, we will explore the implementation of Queues using arrays in C++.

## Table of Contents
- [Introduction to Queues](#introduction-to-queues)
- [Array Implementation of Queues](#array-implementation-of-queues)
- [Operations on Array-based Queues](#operations-on-array-based-queues)
    - [Enqueue](#enqueue)
    - [Dequeue](#dequeue)
    - [Front](#front)
    - [IsEmpty](#isempty)
    - [IsFull](#isfull)
- [Conclusion](#conclusion)

## Introduction to Queues
A Queue is an abstract data type that represents a collection of elements with two main operations - Enqueue, which adds an element to the end of the queue, and Dequeue, which removes an element from the front of the queue. 

## Array Implementation of Queues
One way to implement a Queue is by using an array. In this approach, we use a fixed-size array to store the elements of the queue. 

```cpp
#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    // Operations on Queue
};
```

In the above code snippet, we define a class `Queue` that has a fixed-size array `arr` to store the elements and two integer variables `front` and `rear` to keep track of the front and rear of the queue.

## Operations on Array-based Queues

### Enqueue
The Enqueue operation adds an element to the end of the queue. It checks if the queue is already full before adding the element.

```cpp
void enqueue(int element) {
    if (isFull()) {
        // Handle queue overflow
        return;
    }

    if (isEmpty()) {
        front = 0;
        rear = 0;
    } else {
        rear = (rear + 1) % MAX_SIZE;
    }

    arr[rear] = element;
}
```

### Dequeue
The Dequeue operation removes an element from the front of the queue. It checks if the queue is empty before removing the element.

```cpp
void dequeue() {
    if (isEmpty()) {
        // Handle queue underflow
        return;
    }

    if (front == rear) {
        front = -1;
        rear = -1;
    } else {
        front = (front + 1) % MAX_SIZE;
    }
}
```

### Front
The Front operation returns the element at the front of the queue without removing it. It checks if the queue is empty before accessing the front element.

```cpp
int front() {
    if (isEmpty()) {
        // Handle empty queue
        return -1;
    }

    return arr[front];
}
```

### IsEmpty
The IsEmpty operation checks if the queue is empty by comparing the front and rear indices.

```cpp
bool isEmpty() {
    return (front == -1 && rear == -1);
}
```

### IsFull
The IsFull operation checks if the queue is full. It is full when the rear is one position behind the front.

```cpp
bool isFull() {
    return ((rear + 1) % MAX_SIZE == front);
}
```

## Conclusion
In this blog post, we have seen the implementation of Queues using arrays in C++. Queues have various real-world applications, including CPU scheduling, printer queues, and more. Understanding how to implement queues using arrays is essential for mastering data structures and algorithms.

Hashtags: #queues #datastructures