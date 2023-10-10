---
layout: post
title: "Implement a dequeue operation on a queue in C++"
description: " "
date: 2023-10-10
tags: [Queue]
comments: true
share: true
---

In this blog post, we will explore how to implement a dequeue operation on a queue data structure using C++. A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle, where the element that is inserted first is the one that comes out first.

Let's start by creating a class called `Queue` that will contain the necessary methods and data members to implement a dequeue operation.

```cpp
class Queue {
private:
    int front, rear, size;
    int *arr;
public:
    Queue(int size) {
        front = rear = -1;
        this->size = size;
        arr = new int[size];
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (front == 0 && rear == size - 1) || (front == rear + 1);
    }

    void enqueueFront(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue front." << std::endl;
            return;
        }

        if (front == -1) {
            front = rear = 0;
        } else if (front == 0) {
            front = size - 1;
        } else {
            front--;
        }

        arr[front] = value;

        std::cout << "Enqueued " << value << " at the front of the queue." << std::endl;
    }

    void enqueueRear(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue rear." << std::endl;
            return;
        }

        if (front == -1) {
            front = rear = 0;
        } else if (rear == size - 1) {
            rear = 0;
        } else {
            rear++;
        }

        arr[rear] = value;

        std::cout << "Enqueued " << value << " at the rear of the queue." << std::endl;
    }

    void dequeueFront() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue front." << std::endl;
            return;
        }

        std::cout << "Dequeued " << arr[front] << " from the front of the queue." << std::endl;

        if (front == rear) {
            front = rear = -1;
        } else if (front == size - 1) {
            front = 0;
        } else {
            front++;
        }
    }

    void dequeueRear() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue rear." << std::endl;
            return;
        }

        std::cout << "Dequeued " << arr[rear] << " from the rear of the queue." << std::endl;

        if (front == rear) {
            front = rear = -1;
        } else if (rear == 0) {
            rear = size - 1;
        } else {
            rear--;
        }
    }
};
```

In the code above, we have defined the `Queue` class with a `front` and `rear` pointer to keep track of the indices of the front and rear elements of the queue respectively. We also have a `size` variable to determine the maximum capacity of the queue and an array `arr` to store the elements.

The `isEmpty()` and `isFull()` functions check if the queue is empty or full, respectively. The `enqueueFront()` and `enqueueRear()` functions insert elements at the front and rear of the queue, respectively. The `dequeueFront()` and `dequeueRear()` functions remove elements from the front and rear of the queue, respectively.

To test our implementation, we can create an instance of the `Queue` class and perform enqueue and dequeue operations as follows:

```cpp
int main() {
    Queue queue(5);

    queue.enqueueRear(1);
    queue.enqueueRear(2);
    queue.enqueueFront(3);
    queue.enqueueFront(4);

    queue.dequeueFront();
    queue.dequeueRear();

    return 0;
}
```

By running the above code, we should see the following output:

```
Enqueued 1 at the rear of the queue.
Enqueued 2 at the rear of the queue.
Enqueued 3 at the front of the queue.
Enqueued 4 at the front of the queue.
Dequeued 4 from the front of the queue.
Dequeued 2 from the rear of the queue.
```

In this blog post, we have implemented a dequeue operation on a queue data structure using C++. This allows us to insert and remove elements from both the front and rear of the queue. By having the flexibility of enqueueing and dequeueing from both ends, we can efficiently implement various algorithms and solve problems in computer science.

**#C++ #Queue**