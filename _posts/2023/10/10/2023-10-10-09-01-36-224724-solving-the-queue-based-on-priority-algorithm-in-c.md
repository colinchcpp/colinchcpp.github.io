---
layout: post
title: "Solving the queue based on priority algorithm in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In many real-world applications, we often need to prioritize tasks based on their importance or urgency. One common data structure used to solve this problem is the **priority queue**. In this blog post, we will explore how to implement a priority queue algorithm in C++.

## What is a Priority Queue?

A **priority queue** is an abstract data type that is similar to a regular queue, but with an added feature of prioritizing elements based on a certain criteria. Each element in the priority queue is assigned a priority value, and elements with higher priority values are dequeued before those with lower priority values.

## Implementation of Priority Queue in C++

### Using the Standard Library

C++ provides a built-in implementation of priority queue in the `<queue>` header file. Let's see an example of how to use it:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> pq;

    pq.push(3);
    pq.push(2);
    pq.push(5);
    pq.push(1);

    while(!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop();
    }

    return 0;
}
```

In this example, we create a `std::priority_queue` object called `pq`. We push elements into the priority queue using the `push()` function. The elements are automatically sorted based on their values, with the highest value at the top. We use the `top()` function to access the element with the highest priority, and the `pop()` function to remove it from the queue.

The output of the above code will be: `5 3 2 1`, demonstrating that elements are fetched and removed from the priority queue in descending order based on their priority.

### Custom Priority Queue Implementation

If you need more flexibility or want to prioritize elements based on custom criteria, you can implement your own priority queue class. This can be done using a variety of data structures such as an array, linked list, or heap.

Let's see an example of a custom priority queue implementation using a binary heap:

```cpp
#include <iostream>
#include <vector>

class PriorityQueue {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        while (index > 0) {
            int parentIndex = (index - 1) / 2;
            if (heap[parentIndex] < heap[index]) {
                std::swap(heap[parentIndex], heap[index]);
                index = parentIndex;
            } else {
                break;
            }
        }
    }

    void heapifyDown(int index) {
        int n = heap.size();
        while (2*index+1 < n) {
            int childIndex = 2*index+1;
            if (childIndex+1 < n && heap[childIndex] < heap[childIndex+1]) {
                childIndex++;
            }
            if (heap[index] < heap[childIndex]) {
                std::swap(heap[index], heap[childIndex]);
                index = childIndex;
            } else {
                break;
            }
        }
    }

public:
    void enqueue(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    void dequeue() {
        if (!isEmpty()) {
            heap[0] = heap.back();
            heap.pop_back();
            heapifyDown(0);
        }
    }

    int front() const {
        return heap[0];
    }

    bool isEmpty() const {
        return heap.empty();
    }
};

int main() {
    PriorityQueue pq;

    pq.enqueue(3);
    pq.enqueue(2);
    pq.enqueue(5);
    pq.enqueue(1);

    while (!pq.isEmpty()) {
        std::cout << pq.front() << " ";
        pq.dequeue();
    }

    return 0;
}
```

In this custom priority queue implementation, we use a binary heap to maintain the priority order. Elements are enqueued by adding them to the end of the internal vector, and then restoring the heap property using the `heapifyUp()` function. Dequeuing is done by removing the element at the top of the heap, replacing it with the last element, and then restoring the heap property using the `heapifyDown()` function.

The output of the above code will be: `5 3 2 1`, which is the same as the previous example using the standard library priority queue.

## Conclusion

In this blog post, we explored how to implement a priority queue algorithm in C++. We looked at both the built-in implementation provided by the `<queue>` header file, as well as a custom implementation using a binary heap. Prioritizing tasks based on their importance or urgency is a common requirement in many applications, and the priority queue data structure provides an efficient solution to this problem.