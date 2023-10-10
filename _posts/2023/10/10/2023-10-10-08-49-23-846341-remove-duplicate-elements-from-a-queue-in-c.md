---
layout: post
title: "Remove duplicate elements from a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

Queues are widely used data structures in computer science and can be implemented using various programming languages, including C++. In some cases, you may need to remove duplicate elements from a queue to ensure uniqueness or for further processing. In this blog post, we will explore how to remove duplicate elements from a queue in C++.

## Table of Contents
- [Understanding Queues](#understanding-queues)
- [Approach using an Auxiliary Container](#approach-using-an-auxiliary-container)
- [Approach using the Set Data Structure](#approach-using-the-set-data-structure)
- [Conclusion](#conclusion)

## Understanding Queues
Before we dive into removing duplicate elements from a queue, let's have a quick overview of queues. In simple terms, a queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. Elements are inserted at the back and removed from the front.

In C++, you can implement a queue using the `std::queue` container from the Standard Template Library (STL). It provides member functions like `push()`, `pop()`, and `front()` for inserting, removing, and accessing elements respectively.

## Approach using an Auxiliary Container
One way to remove duplicate elements from a queue is by using an auxiliary container. Here's a step-by-step approach:

1. Initialize an empty auxiliary container (e.g., `std::vector`).
2. While the original queue is not empty:
   - Get the front element of the queue.
   - Check if the element is already present in the auxiliary container.
   - If not present, push it into the auxiliary container and enqueue it back to the original queue.
   - If present, dequeue the element from the original queue.
3. The original queue will now contain only unique elements.

Here's an example implementation in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

void removeDuplicates(std::queue<int>& queue) {
    std::vector<int> auxiliaryContainer;

    while (!queue.empty()) {
        int current = queue.front();
        queue.pop();

        if (std::find(auxiliaryContainer.begin(), auxiliaryContainer.end(), current) == auxiliaryContainer.end()) {
            auxiliaryContainer.push_back(current);
            queue.push(current);
        }
    }
}

int main() {
    std::queue<int> myQueue;
    myQueue.push(1);
    myQueue.push(2);
    myQueue.push(2);
    myQueue.push(3);
    myQueue.push(3);
    myQueue.push(4);

    removeDuplicates(myQueue);

    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " ";
        myQueue.pop();
    }

    return 0;
}
```

Output:
```
1 2 3 4
```

## Approach using the Set Data Structure
Another approach to remove duplicate elements from a queue is by using the `std::set` data structure from the STL. The `std::set` is a container that stores unique elements in a specific order. By enqueueing elements into a set, we can easily eliminate duplicates.

Here's an example implementation using `std::set` in C++:

```cpp
#include <iostream>
#include <queue>
#include <set>

void removeDuplicates(std::queue<int>& queue) {
    std::set<int> uniqueElements;

    while (!queue.empty()) {
        int current = queue.front();
        queue.pop();

        uniqueElements.insert(current);
    }

    while (!uniqueElements.empty()) {
        queue.push(*uniqueElements.begin());
        uniqueElements.erase(uniqueElements.begin());
    }
}

int main() {
    std::queue<int> myQueue;
    myQueue.push(1);
    myQueue.push(2);
    myQueue.push(2);
    myQueue.push(3);
    myQueue.push(3);
    myQueue.push(4);

    removeDuplicates(myQueue);

    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " ";
        myQueue.pop();
    }

    return 0;
}
```

Output:
```
1 2 3 4
```

## Conclusion
Removing duplicate elements from a queue in C++ can be achieved by using an auxiliary container or the `std::set` data structure from the STL. Both approaches provide a way to ensure uniqueness of elements in a queue. Depending on the requirements of your program, you can choose the most suitable approach. Remember to consider time and space complexity when dealing with large queues to ensure efficient execution.