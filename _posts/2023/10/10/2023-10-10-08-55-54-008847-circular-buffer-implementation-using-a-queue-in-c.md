---
layout: post
title: "Circular buffer implementation using a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement a circular buffer using a queue in C++. A circular buffer, also known as a circular queue, is an efficient data structure that allows elements to be inserted and removed in a circular fashion. It has a fixed size and can be used to efficiently process a stream of data.

## What is a Circular Buffer?

A circular buffer is a data structure that follows the First-In-First-Out (FIFO) principle. It has a fixed size, and when the buffer is full, new elements overwrite the oldest elements in a circular fashion. This means that the buffer behaves as if the end and the beginning of the buffer are connected.

## Implementation using a Queue

In C++, we can implement a circular buffer using a queue container from the Standard Template Library (STL). The <queue> library provides a container class template `queue` that implements a queue with its member functions and operations.

Let's take a look at the code snippet below, which demonstrates the implementation of a circular buffer using a queue:

```cpp
#include <iostream>
#include <queue>

class CircularBuffer {
private:
    std::queue<int> buffer;
    int maxSize;

public:
    CircularBuffer(int size) : maxSize(size) {}

    void addElement(int element) {
        if (buffer.size() == maxSize) {
            buffer.pop();
        }
        buffer.push(element);
    }

    void printBuffer() {
        std::queue<int> temp = buffer;
        while (!temp.empty()) {
            std::cout << temp.front() << " ";
            temp.pop();
        }
        std::cout << std::endl;
    }
};

int main() {
    CircularBuffer cb(5);

    cb.addElement(1);
    cb.addElement(2);
    cb.addElement(3);
    cb.addElement(4);
    cb.addElement(5);
    cb.printBuffer(); // Output: 1 2 3 4 5

    cb.addElement(6);
    cb.addElement(7);
    cb.printBuffer(); // Output: 3 4 5 6 7

    return 0;
}
```

In this implementation, we create a `CircularBuffer` class that uses a queue `buffer` to store elements. The `maxSize` variable defines the maximum capacity of the buffer. The class has two member functions: `addElement()` and `printBuffer()`.

The `addElement()` function adds an element to the buffer. If the buffer is already full, the oldest element is removed using the `pop()` function before adding the new element.

The `printBuffer()` function prints the contents of the buffer by creating a temporary copy of the buffer and printing its front element until it becomes empty.

In the `main()` function, we create an instance of the `CircularBuffer` class with a size of 5. We add elements 1 to 5 and print the buffer, which outputs `1 2 3 4 5`. Then, we add two more elements (6 and 7) to the buffer and print it again, this time outputting `3 4 5 6 7` as the oldest elements (1 and 2) have been replaced.

## Conclusion

In this blog post, we have explored how to implement a circular buffer using a queue in C++. The circular buffer is a useful data structure for efficiently storing and processing a stream of data. By using the queue container from the STL, we can easily implement a circular buffer and take advantage of its built-in functionality.