---
layout: post
title: "Implementing a queue with fixed capacity using a circular array in C++"
description: " "
date: 2023-10-10
tags: [datastructures, algorithms]
comments: true
share: true
---

Queues are a fundamental data structure in computer science that follow the First-In-First-Out (FIFO) principle. In some cases, it may be necessary to limit the maximum number of elements that can be stored in a queue.

In this article, we will explore how to implement a queue with fixed capacity using a circular array in C++. This approach allows us to efficiently handle the limited capacity of the queue and utilize the available space effectively.

## Table of Contents
- [Introduction to Circular Array](#introduction-to-circular-array)
- [Implementing a Queue with Fixed Capacity](#implementing-a-queue-with-fixed-capacity)
- [Initializing the Queue](#initializing-the-queue)
- [Enqueue Operation](#enqueue-operation)
- [Dequeue Operation](#dequeue-operation)
- [Full and Empty Checks](#full-and-empty-checks)
- [Conclusion](#conclusion)

## Introduction to Circular Array

A circular array is a data structure where the end of the array is connected to the beginning, forming a continuous loop. This allows us to overcome the limitation of a traditional array where elements cannot be added once the array is full or removed once it is empty.

By using a circular array, we can efficiently manage a fixed-size queue without wasting any unused space.

## Implementing a Queue with Fixed Capacity

Let's begin by implementing the `CircularArrayQueue` class in C++. We will use an array of a fixed size, along with two pointers to indicate the front and rear of the queue.

```cpp
#include <iostream>

class CircularArrayQueue {
private:
  int* arr;         // Array to store the elements
  int capacity;     // Maximum capacity of the queue
  int front;        // Pointer to the front of the queue
  int rear;         // Pointer to the rear of the queue
  int currentSize;  // Current number of elements in the queue

public:
  CircularArrayQueue(int capacity);
  ~CircularArrayQueue();
  void Enqueue(int value);
  int Dequeue();
  bool IsFull();
  bool IsEmpty();
};
```

## Initializing the Queue

To create a circular array queue, we need to allocate memory for the array and initialize the front, rear, and currentSize variables.

```cpp
CircularArrayQueue::CircularArrayQueue(int capacity) {
  this->arr = new int[capacity];
  this->capacity = capacity;
  this->front = 0;
  this->rear = 0;
  this->currentSize = 0;
}
```

## Enqueue Operation

The `Enqueue` operation adds an element to the rear of the queue. If the queue is full, it throws an exception.

```cpp
void CircularArrayQueue::Enqueue(int value) {
  if (IsFull()) {
    throw "Queue is full";
  }

  arr[rear] = value;
  rear = (rear + 1) % capacity;
  currentSize++;
}
```

## Dequeue Operation

The `Dequeue` operation removes and returns the element from the front of the queue. If the queue is empty, it throws an exception.

```cpp
int CircularArrayQueue::Dequeue() {
  if (IsEmpty()) {
    throw "Queue is empty";
  }

  int dequeuedValue = arr[front];
  front = (front + 1) % capacity;
  currentSize--;

  return dequeuedValue;
}
```

## Full and Empty Checks

The `IsFull` and `IsEmpty` methods help us determine if the queue is full or empty, respectively.

```cpp
bool CircularArrayQueue::IsFull() {
  return currentSize == capacity;
}

bool CircularArrayQueue::IsEmpty() {
  return currentSize == 0;
}
```

## Conclusion

By using a circular array, we have implemented a queue with a fixed capacity in C++. This allows us to efficiently manage the memory and utilize the available space effectively.

Implementing data structures like a queue with fixed capacity is essential when dealing with systems that have resource limitations or specific requirements, ensuring that the data structure operates within the desired constraints.

To learn more about data structures and algorithms, check out the [#datastructures](https://example.com/datastructures) and [#algorithms](https://example.com/algorithms) hashtags.