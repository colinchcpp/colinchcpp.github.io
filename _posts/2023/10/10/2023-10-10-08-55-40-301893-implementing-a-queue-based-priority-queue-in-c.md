---
layout: post
title: "Implementing a queue-based priority queue in C++"
description: " "
date: 2023-10-10
tags: [tech]
comments: true
share: true
---

In this blog post, we will explore the implementation of a priority queue using a queue data structure in C++. A priority queue is a data structure that allows elements to be inserted with a priority and retrieved in the order of their priority. We will be using a queue as the underlying data structure for our priority queue implementation.

## Table of Contents
- <a href="#overview">Overview</a>
- <a href="#implementation">Implementation</a>
- <a href="#usage">Usage</a>
- <a href="#conclusion">Conclusion</a>

## <a name="overview"></a>Overview
A priority queue is commonly implemented using a heap data structure, which provides efficient insertion and retrieval operations. However, a queue-based implementation can be a simpler alternative in scenarios where the number of elements is relatively small or the priority needs are not very complex.

## <a name="implementation"></a>Implementation
Let's begin by defining a `PriorityQueue` class that will serve as our queue-based priority queue. In this implementation, we will assume that higher integer values represent higher priorities.

```cpp
#include <queue>

class PriorityQueue {
public:
    void push(int element, int priority) {
        queue.push(std::make_pair(element, priority));
    }

    int pop() {
        int topElement = queue.top().first;
        queue.pop();
        return topElement;
    }

    bool isEmpty() {
        return queue.empty();
    }

private:
    std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>,
        std::function<bool(const std::pair<int, int>&, const std::pair<int, int>&)>> queue{
            [](const std::pair<int, int>& lhs, const std::pair<int, int>& rhs) {
                return lhs.second < rhs.second; // Compare priorities
            }};
};
```

In our implementation, we use the `std::priority_queue` class from the C++ Standard Library as the underlying queue data structure. We define a custom comparator function that compares the priorities of elements.

## <a name="usage"></a>Usage
Let's see how we can use our `PriorityQueue` class to store and retrieve elements with their respective priorities.

```cpp
int main() {
    PriorityQueue pq;

    pq.push(10, 3);
    pq.push(20, 1);
    pq.push(30, 5);
    pq.push(40, 2);

    while (!pq.isEmpty()) {
        int element = pq.pop();
        std::cout << "Popped: " << element << std::endl;
    }
    
    return 0;
}
```

The output of the above code will be:

```
Popped: 30
Popped: 10
Popped: 40
Popped: 20
```

## <a name="conclusion"></a>Conclusion
In this blog post, we have learned how to implement a queue-based priority queue in C++. Although this implementation may not offer the same performance as a heap-based priority queue, it can serve as a simpler alternative in certain scenarios. By using the code provided, you can create your own priority queue and customize it for your specific needs. Happy coding!

#tech #C++