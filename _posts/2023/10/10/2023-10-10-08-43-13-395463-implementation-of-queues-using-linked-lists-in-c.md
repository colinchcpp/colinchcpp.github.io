---
layout: post
title: "Implementation of queues using linked lists in C++"
description: " "
date: 2023-10-10
tags: [datastructures, queues]
comments: true
share: true
---

Queues are a fundamental data structure that follow the First-In-First-Out (FIFO) principle. They are widely used in computer science and can be implemented using various data structures, including arrays and linked lists. In this blog post, we will focus on implementing queues using linked lists in C++.

## Introduction to Linked Lists

A linked list is a data structure consisting of a collection of nodes, where each node contains a value and a pointer to the next node. Unlike arrays, linked lists do not have a fixed size and can dynamically grow or shrink as elements are added or removed. This flexibility makes linked lists a suitable choice for implementing queues.

## Queue Operations

Before diving into the implementation, let's first define the basic operations that can be performed on a queue:

1. `enqueue(x)`: Insert an element `x` at the rear of the queue.
2. `dequeue()`: Remove and return the element at the front of the queue.
3. `isEmpty()`: Check if the queue is empty.
4. `size()`: Get the number of elements currently in the queue.
5. `front()`: Get the element at the front of the queue without removing it.

## Implementing Queues Using Linked Lists in C++

To implement a queue using a linked list, we need to define a `Node` structure to represent each element of the queue. Each `Node` will contain a value and a pointer to the next node.

```cpp
class Node {
public:
    int data;
    Node* next;
};
```

Next, we define a `Queue` class that contains pointers to the front and rear nodes of the linked list.

```cpp
class Queue {
private:
    Node* front;
    Node* rear;
public:
    Queue();
    ~Queue();
    
    void enqueue(int x);
    int dequeue();
    bool isEmpty();
    int size();
    int front();
};
```

Let's implement the enqueue operation which adds an element to the rear of the queue.

```cpp
void Queue::enqueue(int x) {
    Node* newNode = new Node();
    newNode->data = x;
    newNode->next = nullptr;
    
    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
}
```

The dequeue operation removes and returns the element from the front of the queue.

```cpp
int Queue::dequeue() {
    if (isEmpty()) {
        throw runtime_error("Queue is empty");
    }
    
    int value = front->data;
    Node* temp = front;
    front = front->next;
    
    if (front == nullptr) {
        rear = nullptr;
    }
    
    delete temp;
    return value;
}
```

The isEmpty operation checks if the queue is empty.

```cpp
bool Queue::isEmpty() {
    return front == nullptr;
}
```

The size operation returns the number of elements in the queue.

```cpp
int Queue::size() {
    int count = 0;
    Node* current = front;
    
    while (current != nullptr) {
        count++;
        current = current->next;
    }
    
    return count;
}
```

The front operation returns the value of the element at the front of the queue without removing it.

```cpp
int Queue::front() {
    if (isEmpty()) {
        throw runtime_error("Queue is empty");
    }
    
    return front->data;
}
```

## Conclusion

In this blog post, we learned about the implementation of queues using linked lists in C++. We discussed the basic operations of queues and provided a complete implementation using a linked list data structure.

By understanding how queues work and how they can be implemented using linked lists, you can utilize this knowledge to solve a wide range of problems that require a FIFO data structure.

Happy coding!

**#datastructures #queues**