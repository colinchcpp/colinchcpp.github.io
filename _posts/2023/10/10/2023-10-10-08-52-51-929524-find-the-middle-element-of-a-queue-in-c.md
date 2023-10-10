---
layout: post
title: "Find the middle element of a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

When working with queues in C++, you might have a scenario where you need to find the middle element of the queue. This could be useful, for example, when implementing a priority queue and you want to access the middle element for certain operations.

In this blog post, we will explore an efficient approach to find the middle element of a queue in C++. Let's get started!

### Approach

To find the middle element of a queue, we can use two additional queues: `tempQueue` and `middleQueue`. We will traverse the original queue and simultaneously enqueue the elements into the `tempQueue`. However, before enqueuing each element into `tempQueue`, we first check if `tempQueue` has already half of the elements of the original queue. If so, we enqueue the front element of `tempQueue` into `middleQueue`.

Here's the step-by-step algorithm:

1. Create an empty queue called `tempQueue` and `middleQueue`.
2. Traverse the original queue:
   - Enqueue each element into `tempQueue`.
   - Check if `tempQueue` has already half of the elements of the original queue.
   - If so, enqueue the front element of `tempQueue` into `middleQueue`.
3. Finally, the front element of `middleQueue` will be the middle element of the original queue.

### Implementation

```cpp
#include <iostream>
#include <queue>

// Function to find the middle element of a queue
int findMiddleElement(std::queue<int>& q) {
    std::queue<int> tempQueue, middleQueue;
    int count = 0;
    int middleElement = 0;

    // Traverse the original queue
    while (!q.empty()) {
        // Enqueue each element into the tempQueue
        tempQueue.push(q.front());
        q.pop();

        count++;
        // Check if tempQueue has already half of the elements of the original queue
        if (count % 2 == 0) {
            // Enqueue the front element of tempQueue into middleQueue
            middleQueue.push(tempQueue.front());
            tempQueue.pop();
        }
    }

    // Get the middle element from middleQueue
    if (!middleQueue.empty()) {
        middleElement = middleQueue.front();
    }

    return middleElement;
}

int main() {
    std::queue<int> q;
    q.push(10);
    q.push(20);
    q.push(30);
    q.push(40);
    q.push(50);

    int middleElement = findMiddleElement(q);

    std::cout << "Middle element of the queue: " << middleElement << std::endl;

    return 0;
}
```

### Conclusion

In this blog post, we learned how to find the middle element of a queue in C++ using an efficient approach. By leveraging two additional queues, we can easily access the middle element of a queue without going through the entire queue.

Using this approach, you can now incorporate finding the middle element of a queue in your C++ programs efficiently.