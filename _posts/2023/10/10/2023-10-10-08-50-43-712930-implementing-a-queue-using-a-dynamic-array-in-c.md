---
layout: post
title: "Implementing a queue using a dynamic array in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this article, we will explore how to implement a queue data structure using a dynamic array in C++. A queue is a type of data structure that follows the First-In-First-Out (FIFO) principle, where the element that is added first will be the first one to be removed.

### What is a Queue?

A queue is a linear data structure that consists of two main operations: enqueue and dequeue. The enqueue operation adds an element to the end of the queue, while the dequeue operation removes the element from the front of the queue. This makes queues particularly useful when dealing with tasks that need to be processed in a specific order.

### Dynamic Array

A dynamic array, also known as a resizable array, is an array whose size can be dynamically adjusted during runtime. In C++, we can implement a dynamic array using pointers and allocating memory using the `new` keyword. This allows us to resize the array as needed.

### Implementation

Let's start by creating a `Queue` class that will hold the necessary methods and attributes to implement the queue using a dynamic array.

```cpp
class Queue {
private:
    int* arr;
    int front;
    int rear;
    int capacity;
    int size;

public:
    Queue(int capacity) {
        this->capacity = capacity;
        arr = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == capacity;
    }

    void enqueue(int item) {
        if (isFull()) {
            // Dynamically resize the array
            int* newArr = new int[2 * capacity];

            for (int i = 0; i < size; i++) {
                newArr[i] = arr[(front + i) % capacity];
            }

            capacity *= 2;

            delete[] arr;
            arr = newArr;
            front = 0;
            rear = size - 1;
        }

        rear = (rear + 1) % capacity;
        arr[rear] = item;
        size++;
    }

    int dequeue() {
        if (isEmpty()) {
            throw "Queue is empty";
        }

        int item = arr[front];
        front = (front + 1) % capacity;
        size--;

        return item;
    }
};
```

In the above implementation, we have defined the necessary methods such as `isEmpty`, `isFull`, `enqueue`, and `dequeue` to interact with the queue.

### Testing the Queue Implementation

Now, let's write a small program to test our queue implementation.

```cpp
int main() {
    Queue queue(5);

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    queue.enqueue(40);
    queue.enqueue(50);
    queue.enqueue(60);
    queue.enqueue(70);

    while (!queue.isEmpty()) {
        cout << "Dequeued item: " << queue.dequeue() << endl;
    }

    return 0;
}
```

The output of the above code should be:

```
Dequeued item: 10
Dequeued item: 20
Dequeued item: 30
Dequeued item: 40
Dequeued item: 50
Dequeued item: 60
Dequeued item: 70
```

### Conclusion

In this article, we learned how to implement a queue data structure using a dynamic array in C++. By dynamically resizing the array when it becomes full, we ensure that the queue can expand as needed and efficiently handle any number of elements. Using this implementation, you can now incorporate queues into your C++ programs and solve problems that require FIFO operations.