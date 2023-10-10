---
layout: post
title: "Basic operations on queues (enqueue and dequeue)"
description: " "
date: 2023-10-10
tags: [queue, datastructure]
comments: true
share: true
---

Queues are a fundamental data structure that follows the First-In-First-Out (FIFO) principle. In this blog post, we will explore the basic operations on queues – enqueue and dequeue. These operations allow us to add elements to the queue and remove elements from the queue, respectively.

## Table of Contents
- [Introduction](#introduction)
- [Enqueue Operation](#enqueue-operation)
- [Dequeue Operation](#dequeue-operation)
- [Implementation in Python](#implementation-in-python)
- [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

A queue can be visualized as a line of people waiting for something. The person who arrives first gets served first, and new people join the queue at the back. Similarly, the first element added to a queue is the first one to be removed.

## Enqueue Operation <a name="enqueue-operation"></a>

The enqueue operation adds an element to the end of the queue. It is equivalent to someone joining the line. The newly added element becomes the last element of the queue.

## Dequeue Operation <a name="dequeue-operation"></a>

The dequeue operation removes an element from the front of the queue. It is equivalent to the person at the front of the line getting served and leaving. The element removed is the oldest one in the queue.

## Implementation in Python <a name="implementation-in-python"></a>

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        self.queue.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.queue.pop(0)
        return None
    
    def is_empty(self):
        return len(self.queue) == 0

    def size(self):
        return len(self.queue)
```

In the above code snippet, we define a `Queue` class that includes methods for enqueue, dequeue, checking if the queue is empty, and getting the size of the queue. The `enqueue` method appends the item to the end of the list, and the `dequeue` method removes the first item from the list.

## Conclusion <a name="conclusion"></a>

Understanding the basics of queues and their operations is crucial for handling data in various applications. The enqueue operation allows us to add elements to the end of the queue, while the dequeue operation helps us remove elements from the front of the queue. By implementing these operations, we can efficiently manage data in a FIFO manner.

#queue #datastructure