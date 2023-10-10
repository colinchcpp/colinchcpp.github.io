---
layout: post
title: "Introduction to queues in C++"
description: " "
date: 2023-10-10
tags: [peek, cplusplus]
comments: true
share: true
---

Queues are an essential data structure in computer science that follows the principle of "First-In-First-Out" (FIFO). In other words, the elements that are inserted first are the ones that are removed first. Queues are used in various applications, including job scheduling, task management, and network communication.

In this blog post, we will explore the basics of implementing queues in C++. We will cover the fundamental operations of a queue, such as enqueue, dequeue, and peek, as well as discuss some common use cases.

## Table of Contents
- [Queue Implementation](#queue-implementation)
- [Enqueue Operation](#enqueue-operation)
- [Dequeue Operation](#dequeue-operation)
- [Peek Operation](#peek-operation)
- [Use Cases](#use-cases)

## Queue Implementation {#queue-implementation}

In C++, queues can be implemented using various data structures. One of the commonly used approaches is to implement a queue using a linked list. Each node in the linked list represents an element in the queue, and the head and tail pointers keep track of the first and last elements, respectively.

```cpp
class Node {
public:
    int data;
    Node* next;
    
    Node(int value) {
        data = value;
        next = nullptr;
    }
};

class Queue {
private:
    Node* head;
    Node* tail;

public:
    Queue() {
        head = nullptr;
        tail = nullptr;
    }

    // Other operations will be implemented here
};
```

## Enqueue Operation {#enqueue-operation}

The enqueue operation adds an element to the end of the queue. To enqueue an element, we create a new node and update the tail pointer to point to this new node. If the queue is empty, we update both the head and tail pointers.

```cpp
void enqueue(int value) {
    Node* newNode = new Node(value);
    
    if (isEmpty()) {
        head = newNode;
        tail = newNode;
    } else {
        tail->next = newNode;
        tail = newNode;
    }
}
```

## Dequeue Operation {#dequeue-operation}

The dequeue operation removes the element from the front of the queue. To dequeue an element, we update the head pointer to the next node in the queue. If the queue becomes empty after dequeuing, we update both the head and tail pointers to nullptr.

```cpp
void dequeue() {
    if (isEmpty()) {
        // Handle underflow condition
        return;
    }
    
    Node* temp = head;
    head = head->next;

    delete temp;

    if (isEmpty()) {
        tail = nullptr;
    }
}
```

## Peek Operation {#peek-operation}

The peek operation allows us to access the element at the front of the queue without removing it. To peek an element, we simply return the value of the node pointed by the head pointer.

```cpp
int peek() {
    if (isEmpty()) {
        // Handle underflow condition
        return -1;
    }

    return head->data;
}
```

## Use Cases {#use-cases}

Queues find applications in scenarios where maintaining the order of elements is crucial. Some common use cases include:

1. **Job Scheduling**: Queues are used to manage the execution order of jobs in a system. The jobs are placed in a queue, and the system processes them one by one based on the FIFO principle.

2. **Waiting Lines**: Queues are used to model waiting lines, such as customer queues in banks, ticket counters, or call centers. The customers join the queue and are served in the order they arrived.

By understanding the basics of implementing queues in C++, you can leverage this data structure to build efficient and organized solutions for various problems.

#cplusplus #queues