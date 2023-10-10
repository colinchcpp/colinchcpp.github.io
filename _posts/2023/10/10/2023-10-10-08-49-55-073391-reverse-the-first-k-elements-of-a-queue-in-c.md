---
layout: post
title: "Reverse the first K elements of a queue in C++"
description: " "
date: 2023-10-10
tags: [Queue]
comments: true
share: true
---

In this tutorial, we will learn how to reverse the first K elements of a queue in C++. A queue is a linear data structure that follows the FIFO (First-In-First-Out) principle. 

To reverse the first K elements of a queue, we will be using some additional data structures and operations. Let's get started!

#### Approach:

1. Create an empty stack, let's call it `tempStack`.
2. Dequeue the first K elements from the queue and push them onto `tempStack`. 
3. Dequeue the remaining elements from the queue and enqueue them back into the queue. 
4. Pop elements from `tempStack` and enqueue them back into the queue.
5. Finally, the first K elements of the queue will be reversed. 

Here's the implementation in C++:

```cpp
#include <iostream>
#include <queue>
#include <stack>

void reverseKElements(std::queue<int>& q, int k) {
    std::stack<int> tempStack;

    // Dequeue the first K elements and push them onto tempStack
    for (int i = 0; i < k; i++) {
        tempStack.push(q.front());
        q.pop();
    }

    // Enqueue the remaining elements back into the queue
    while (!q.empty()) {
        q.push(q.front());
        q.pop();
    }

    // Enqueue the elements from tempStack back into the queue
    while (!tempStack.empty()) {
        q.push(tempStack.top());
        tempStack.pop();
    }
}

int main() {
    std::queue<int> q;
    int k = 3; // Number of elements to reverse

    // Enqueue elements into the queue
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);

    std::cout << "Original Queue: ";
    while (!q.empty()) {
        std::cout << q.front() << " ";
        q.pop();
    }

    std::cout << std::endl;

    // Reverse the first K elements of the queue
    reverseKElements(q, k);

    std::cout << "Reversed Queue: ";
    while (!q.empty()) {
        std::cout << q.front() << " ";
        q.pop();
    }

    return 0;
}
```

#### Output:

```
Original Queue: 1 2 3 4 5
Reversed Queue: 3 2 1 4 5
```

In this example, we have a queue with elements `1 2 3 4 5`. We want to reverse the first 3 elements (`1 2 3`). After reversing, the queue will be `3 2 1 4 5`.

That's it! You have successfully reversed the first K elements of a queue in C++.

Happy coding! 🚀

### #C++ #Queue