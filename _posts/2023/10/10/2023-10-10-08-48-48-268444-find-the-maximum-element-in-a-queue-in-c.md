---
layout: post
title: "Find the maximum element in a queue in C++"
description: " "
date: 2023-10-10
tags: [Queue]
comments: true
share: true
---

To find the maximum element, we can use an auxiliary data structure such as a max-heap. A max-heap is a complete binary tree where the value of each node is greater than or equal to the values of its children. By maintaining a max-heap alongside the queue, we can easily keep track of the maximum element.

Let's dive into the code:

```cpp
#include <iostream>
#include <queue>

// Function to find the maximum element in a queue
int findMaxInQueue(std::queue<int>& q) {
    std::priority_queue<int> maxHeap;

    // Insert all elements from queue into max-heap
    while (!q.empty()) {
        int element = q.front();
        q.pop();
        maxHeap.push(element);
    }

    // The maximum element is at the top of the max-heap
    int maxElement = maxHeap.top();
    return maxElement;
}

int main() {
    std::queue<int> queue;
    queue.push(3);
    queue.push(6);
    queue.push(2);
    queue.push(8);
    queue.push(1);

    int maxElement = findMaxInQueue(queue);
    std::cout << "Maximum element in the queue: " << maxElement << std::endl;

    return 0;
}
```

In the code snippet above, we first include the necessary headers (`<iostream>` and `<queue>`). Then, we define a function `findMaxInQueue` that takes a reference to a `std::queue<int>`. Inside the function, we create a `std::priority_queue<int>`, which acts as our max-heap.

We iterate over all elements in the queue and insert them into the max-heap using the `push` function. Once we have inserted all elements, the maximum element can be obtained from the top of the max-heap using the `top` function.

In the `main` function, we create a queue and push a few elements into it. We then call the `findMaxInQueue` function and output the result.

By using a max-heap, we can find the maximum element in a queue efficiently with a time complexity of O(n log n), where n is the number of elements in the queue.

I hope you find this article helpful in finding the maximum element in a queue in C++. If you have any queries, feel free to leave a comment below.

#C++ #Queue