---
layout: post
title: "Initializing std::priority_queue using uniform initialization in C++"
description: " "
date: 2023-10-24
tags: [cplusplus, datastructures]
comments: true
share: true
---

In C++, the `std::priority_queue` is a container adapter class that provides a priority queue implementation. It is typically implemented as a max heap, where elements with higher priority are dequeued first. 

Traditionally, the `std::priority_queue` is initialized using the constructor. However, with the introduction of uniform initialization syntax in C++11, we can now initialize it using the curly brace initializer syntax.

Here's an example of how to initialize a `std::priority_queue` using uniform initialization in C++:

```cpp
#include <queue>

int main() {
    std::priority_queue<int> pq {9, 4, 6, 2, 7};

    // Accessing the top element
    int topElement = pq.top();
    
    // Printing the elements in the priority queue
    while (!pq.empty()) {
        int element = pq.top();
        pq.pop();
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In the above code, we create a `std::priority_queue` called `pq` and initialize it using the uniform initialization syntax `{9, 4, 6, 2, 7}`. This inserts the numbers 9, 4, 6, 2, and 7 into the priority queue.

We can then access the top element of the priority queue using the `top()` function, which returns a reference to the highest priority element.

To print the elements in the priority queue, we use a loop that iterates until the queue is empty. In each iteration, we retrieve the top element, print it, and then remove it from the queue using the `pop()` function.

When executed, the output will be: `9 7 6 4 2`, showing that the elements are dequeued in descending order, as expected from a max heap.

Using uniform initialization to initialize a `std::priority_queue` allows for a more concise and readable code. It is worth noting that the underlying container used by `std::priority_queue` is `std::vector` by default. If you want to use a different container, you can specify it as the second template argument.

For more information on `std::priority_queue` and its member functions, refer to the [C++ documentation](https://en.cppreference.com/w/cpp/container/priority_queue).

**#cplusplus #datastructures**