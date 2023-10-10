---
layout: post
title: "Check if a queue can be sorted into another queue in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

When working with queues in C++, you may come across situations where you need to check if one queue can be sorted into another queue. In this blog post, we will explore an algorithm to determine if a given queue can be sorted into a specific order, using C++.

## Problem Description
The problem can be stated as follows: Given two queues A and B, we want to check if queue A can be sorted into the same order as queue B.

## Approach
To solve this problem, we can use the following approach:
1. Create an auxiliary stack.
2. Loop through the elements of queue A and do the following for each element.
    - If the front element of queue A is equal to the front element of queue B, remove both elements from both queues.
    - If the front element of queue A is not equal to the front element of queue B, push the front element of queue A onto the stack.
3. After the loop, if both queues are empty, it means queue A can be sorted into queue B. If not, pop elements from the stack and compare with the elements of queue B until the stack is empty or the elements are not equal.

## Example Code

```cpp
#include <iostream>
#include <queue>
#include <stack>

bool canSortQueue(std::queue<int>& queueA, std::queue<int>& queueB) {
    std::stack<int> auxStack;

    while (!queueA.empty()) {
        if (queueA.front() == queueB.front()) {
            queueA.pop();
            queueB.pop();
        } else {
            auxStack.push(queueA.front());
            queueA.pop();
        }
    }

    while (!stack.empty() && !queueB.empty()) {
        if (auxStack.top() == queueB.front()) {
            auxStack.pop();
            queueB.pop();
        } else {
            return false; // Elements are not equal
        }
    }

    return queueA.empty() && auxStack.empty() && queueB.empty();
}

int main() {
    std::queue<int> queueA;
    std::queue<int> queueB;

    queueA.push(1);
    queueA.push(2);
    queueA.push(3);

    queueB.push(2);
    queueB.push(1);
    queueB.push(3);

    if (canSortQueue(queueA, queueB)) {
        std::cout << "Queue A can be sorted into Queue B" << std::endl;
    } else {
        std::cout << "Queue A cannot be sorted into Queue B" << std::endl;
    }

    return 0;
}
```

## Conclusion
In this blog post, we discussed an algorithm to check if one queue can be sorted into another queue in C++. By using an auxiliary stack, we compared the elements of the queues and determined the sorting possibility. Feel free to use the provided code as a starting point for your own projects.

#programming #C++