---
layout: post
title: "Design a circular queue with a dynamic resizing feature in C++"
description: " "
date: 2023-10-10
tags: [datastructures]
comments: true
share: true
---

In this article, we will learn how to design a circular queue data structure with a dynamic resizing feature using C++. A circular queue is a data structure that follows the First-In-First-Out (FIFO) principle. It is similar to a normal queue, with the difference being that the last element is connected to the first element. Adding elements after the last position in a circular queue simply wraps around to the beginning of the queue.

## Table of Contents
- [Introduction to Circular Queue](#introduction-to-circular-queue)
- [Designing the CircularQueue Class](#designing-the-circularqueue-class)
- [Implementing the Dynamic Resizing Feature](#implementing-the-dynamic-resizing-feature)
- [Conclusion](#conclusion)

## Introduction to Circular Queue

A circular queue is typically implemented using an array and two pointers, a front pointer, and a rear pointer. The front pointer represents the position of the first element in the queue, while the rear pointer represents the position where the next element will be inserted. Initially, both pointers are set to -1.

When the rear pointer reaches the end of the array, it wraps around to the beginning of the array. Similarly, when the front pointer reaches the end of the array, it also wraps around to the beginning of the array. This wrapping behavior gives the circular queue its name.

## Designing the CircularQueue Class

Let's start by designing the `CircularQueue` class. Here's a basic implementation of the class with its member variables and methods:

```cpp
class CircularQueue {
private:
    int* queue;  // array to store elements
    int front;   // index of the front element
    int rear;    // index of the rear element
    int capacity;  // maximum capacity of the queue
    int size;     // current size of the queue

public:
    // Constructor
    CircularQueue(int capacity);

    // Destructor
    ~CircularQueue();

    // Method to add an element to the queue
    void enqueue(int value);

    // Method to remove an element from the queue
    void dequeue();

    // Method to get the front element of the queue
    int getFront();

    // Method to check if the queue is empty
    bool isEmpty();

    // Method to check if the queue is full
    bool isFull();
};
```

In this implementation, we have the `queue` variable to store the elements, `front` and `rear` variables to keep track of the indices, `capacity` to store the maximum capacity of the queue, and `size` to store the current size of the queue.

## Implementing the Dynamic Resizing Feature

To implement the dynamic resizing feature, we need to modify the `enqueue` method. Whenever the queue is full, instead of discarding new elements, we will resize the queue by doubling its capacity and copying the elements to the new larger queue.

Here's an updated version of the `enqueue` method:

```cpp
void CircularQueue::enqueue(int value) {
    // Check if the queue is full
    if (isFull()) {
        // Create a new queue with double the capacity
        int newCapacity = capacity * 2;
        int* newQueue = new int[newCapacity];

        // Copy the elements to the new queue
        for (int i = 0; i < capacity; i++) {
            newQueue[i] = queue[front];
            front = (front + 1) % capacity;
        }

        // Update the front and rear pointers and capacity
        front = 0;
        rear = capacity;
        capacity = newCapacity;

        // Delete the old queue
        delete[] queue;

        // Assign the new queue to the queue variable
        queue = newQueue;
    }

    // Add the new element at the rear position and update the rear pointer
    queue[rear] = value;
    rear = (rear + 1) % capacity;
    size++;
}
```

In this updated implementation, we first create a new queue with double the capacity. We then copy the elements from the old queue to the new queue while updating the front pointer accordingly. After that, we update the front, rear, and capacity variables accordingly. Finally, we delete the old queue and assign the new queue to the `queue` variable.

## Conclusion

In this article, we have learned how to design a circular queue with a dynamic resizing feature using C++. The dynamic resizing feature allows the circular queue to automatically resize itself when it reaches its maximum capacity, ensuring that no elements are discarded. This enables the circular queue to efficiently handle a variable number of elements and avoid unnecessary memory waste.

By implementing the CircularQueue class and the dynamic resizing feature as described, you can use this versatile data structure in your C++ projects. Remember to always test your code thoroughly to ensure its correctness and efficiency.

**#c++ #datastructures**