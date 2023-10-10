---
layout: post
title: "Reverse alternate K nodes in a queue in C++"
description: " "
date: 2023-10-10
tags: [programming, Cplusplus]
comments: true
share: true
---

In this blog post, we will discuss a common problem of reversing alternate K nodes in a queue using C++. We will go through the step-by-step process to solve this problem efficiently.

## Problem Statement

Given a queue of integers and a positive integer K, we need to reverse the order of alternate K nodes in the queue. For example, if the input queue is [1, 2, 3, 4, 5, 6, 7, 8, 9] and K is 2, the output queue should be [2, 1, 3, 4, 6, 5, 7, 8, 9] after reversing alternate 2 nodes, starting from the front of the queue.

## Approach

To solve this problem, we can use a stack to temporarily store the elements that need to be reversed. We will iterate through the elements of the queue, and for every alternate K nodes, we will push them into the stack. Once we have processed K nodes, we will pop the elements from the stack and enqueue them back into the queue in reverse order.

## Implementation

Let's take a look at the C++ code implementation for reversing alternate K nodes in a queue:

```cpp
#include <iostream>
#include <queue>
#include <stack>

void reverseAlternateKNodes(std::queue<int>& q, int k) {
    std::stack<int> s;
    int currentCount = 0;
  
    while (!q.empty()) {
        if (currentCount < k) {
            s.push(q.front());
            q.pop();
            currentCount++;
        } else {
            while (!s.empty()) {
                q.push(s.top());
                s.pop();
            }
            currentCount = 0;
        }
    }

    // Enqueue remaining elements from the stack if the count is odd
    if (currentCount % 2 != 0) {
        int lastElement = s.top();
        s.pop();
        q.push(lastElement);
    }
}

int main() {
    std::queue<int> q;
    int k = 2;
  
    // Enqueue elements into the queue
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);
    q.push(6);
    q.push(7);
    q.push(8);
    q.push(9);

    std::cout << "Original Queue: ";
    while (!q.empty()) {
        std::cout << q.front() << " ";
        q.pop();
    }

    std::cout << std::endl;

    reverseAlternateKNodes(q, k);

    std::cout << "Modified Queue: ";
    while (!q.empty()) {
        std::cout << q.front() << " ";
        q.pop();
    }

    return 0;
}
```

## Explanation

The `reverseAlternateKNodes` function takes a reference to a queue and the value of K as parameters. Inside the function, we create an empty stack `s` to store the elements that need to be reversed.

We then iterate through the elements of the queue using a while loop. For each element, we check the value of `currentCount` and perform the following actions:

- If `currentCount` is less than K, we push the front element of the queue into the stack `s`, pop it from the queue, and increment `currentCount`.
- If `currentCount` is equal to K, we enter a nested while loop and pop the elements from the stack `s` and enqueue them back into the queue. We then reset `currentCount` to 0.
- After processing all the elements in the queue, we check if the count is odd. If so, we pop the top element from the stack and enqueue it back into the queue.

In the `main` function, we create a queue `q` and enqueue the elements [1, 2, 3, 4, 5, 6, 7, 8, 9] into it. We then call the `reverseAlternateKNodes` function to reverse alternate K nodes (where K is set to 2) in the queue. Finally, we print the modified queue.

## Conclusion

We have discussed the efficient approach to reverse alternate K nodes in a queue using C++. By using a stack to temporarily store the elements to be reversed, we can solve this problem with a time complexity of O(n), where n is the size of the queue.

You can find the complete code implementation [here](https://gist.github.com/example).

#programming #Cplusplus