---
layout: post
title: "Implementing a queue with fixed window size in C++"
description: " "
date: 2023-10-10
tags: [cplusplus, datastructures]
comments: true
share: true
---

A queue is a fundamental data structure in computer science that follows the First-In-First-Out (FIFO) principle. In certain scenarios, you may need to implement a queue with a fixed window size, where elements added to the queue beyond the fixed size will cause the oldest elements to be removed.

In this blog post, we will discuss how to implement a queue with a fixed window size in C++. Let's dive in!

## Queue Class Implementation

First, let's define a queue class that supports the required functionality. We'll call this class `FixedSizeQueue`. Here is the implementation:

```cpp
#include <queue>

template <typename T>
class FixedSizeQueue {
private:
    std::queue<T> queue;
    size_t maxSize;

public:
    FixedSizeQueue(size_t size)
        : maxSize(size) {}

    void enqueue(const T& element) {
        if (queue.size() >= maxSize) {
            queue.pop();
        }
        queue.push(element);
    }

    T dequeue() {
        T element = queue.front();
        queue.pop();
        return element;
    }

    size_t size() const {
        return queue.size();
    }

    bool empty() const {
        return queue.empty();
    }
};
```

## Usage Example

Let's demonstrate how to use the `FixedSizeQueue` class with a fixed size of 3:

```cpp
#include <iostream>

int main() {
    FixedSizeQueue<int> queue(3);

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    std::cout << "Queue size: " << queue.size() << std::endl;  // Output: Queue size: 3

    queue.enqueue(4);
    std::cout << "Queue size: " << queue.size() << std::endl;  // Output: Queue size: 3

    int firstElement = queue.dequeue();
    std::cout << "Dequeued element: " << firstElement << std::endl;  // Output: Dequeued element: 2

    return 0;
}
```

In the above example, we create a `FixedSizeQueue` object with a maximum size of 3. We enqueue elements 1, 2, and 3, and then the queue reaches its maximum size. When we try to enqueue the fourth element (4), the oldest element (1) is automatically dequeued. Finally, we dequeue the first element (2) manually.

## Conclusion

Implementing a queue with a fixed window size can be useful in scenarios where you need to limit the number of elements in a queue. In this blog post, we discussed how to implement such a queue in C++ using a `FixedSizeQueue` class. Feel free to use the provided code as a starting point for your own implementations.

Hashtags: #cplusplus #datastructures