---
layout: post
title: "Implementing a queue using a binary heap in C++"
description: " "
date: 2023-10-10
tags: [datastructures]
comments: true
share: true
---

In this article, we will explore how to implement a queue data structure using a binary heap in C++. Queues are commonly used in computer science applications to store and manage data in a FIFO (First-In-First-Out) manner.

A binary heap is a binary tree with two properties: heap order property and shape property. The heap order property ensures that each parent node has a value less than or equal to its child nodes, while the shape property ensures that the tree is a complete binary tree.

To implement a queue using a binary heap, we will use an array to store the elements, where each element represents a node in the binary heap. We will perform heap operations such as enqueue and dequeue to maintain the heap properties.

Let's start by defining our Queue class that will utilize the binary heap implementation:

```cpp
#include <iostream>
#include <vector>

class Queue {
private:
    std::vector<int> heap;

    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    void bubbleUp(int index) {
        while (index > 0 && heap[(index - 1) / 2] > heap[index]) {
            swap(heap[index], heap[(index - 1) / 2]);
            index = (index - 1) / 2;
        }
    }

    void bubbleDown(int index) {
        int smallest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        if (left < heap.size() && heap[left] < heap[smallest])
            smallest = left;

        if (right < heap.size() && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            bubbleDown(smallest);
        }
    }

public:
    void enqueue(int value) {
        heap.push_back(value);
        bubbleUp(heap.size() - 1);
    }

    int dequeue() {
        if (heap.empty()) {
            std::cout << "Error: Queue is empty!" << std::endl;
            return -1;
        }

        int front = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        bubbleDown(0);

        return front;
    }

    bool isEmpty() {
        return heap.empty();
    }
};
```

The `Queue` class consists of a private member variable `heap`, which is a vector used as the underlying data structure for our binary heap implementation. The `swap` function is a helper function to swap two elements in the heap. The `bubbleUp` function maintains the heap's order property by continuously swapping the element with its parent until it reaches the correct position. Similarly, the `bubbleDown` function maintains the heap's order property by continuously swapping the element with its smallest child until it reaches the correct position.

The public member functions include `enqueue`, `dequeue`, and `isEmpty` for adding an element to the queue, removing an element from the queue, and checking if the queue is empty, respectively.

Now we can use our `Queue` class to create a queue and perform enqueue and dequeue operations:

```cpp
int main() {
    Queue queue;

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    std::cout << "Dequeued element: " << queue.dequeue() << std::endl;

    queue.enqueue(40);

    while (!queue.isEmpty()) {
        std::cout << "Dequeued element: " << queue.dequeue() << std::endl;
    }

    return 0;
}
```

The output of the above code will be:

```
Dequeued element: 10
Dequeued element: 20
Dequeued element: 30
Dequeued element: 40
```

In this article, we implemented a queue data structure using a binary heap in C++. This implementation provides an efficient way to perform enqueue and dequeue operations in O(log n) time complexity, where n is the number of elements in the queue.

I hope you found this article helpful. Happy coding!

\#datastructures #c++