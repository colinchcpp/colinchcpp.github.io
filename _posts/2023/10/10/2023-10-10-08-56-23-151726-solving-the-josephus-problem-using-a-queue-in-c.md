---
layout: post
title: "Solving the Josephus problem using a queue in C++"
description: " "
date: 2023-10-10
tags: [tags, queue]
comments: true
share: true
---

The Josephus problem is a famous mathematical problem. It is described as follows: *n* people are standing in a circle, and starting from a given position, every *k*-th person is executed, where *k* is a positive integer. The process continues until only one person is left. The task is to find the position of the last person standing.

One of the efficient ways to solve the Josephus problem is by using a queue data structure. In this blog post, we'll walk through the implementation of the Josephus problem using a queue in C++.

## The Queue Data Structure

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. Elements are added at the rear (also known as enqueue) and removed from the front (also known as dequeue) of the queue.

In C++, the `std::queue` class from the `<queue>` library provides a ready-to-use implementation of a queue. It supports various operations such as `push()`, `pop()`, `front()`, `back()`, `size()`, etc.

## Implementation

Let's start by including the necessary libraries and declaring our main function:

```cpp
#include <iostream>
#include <queue>

int main() {
    int n, k;
    std::cout << "Enter the number of people (n): ";
    std::cin >> n;
    std::cout << "Enter the value of k: ";
    std::cin >> k;

    std::queue<int> q;
    for (int i = 1; i <= n; i++) {
        q.push(i);
    }
    
    // Rest of the logic goes here
    
    return 0;
}
```

In the above code, we take input for the number of people (`n`) and the value of `k`. We then create a queue `q` and add numbers from 1 to `n` to the queue.

Next, we need to simulate the Josephus problem by repeatedly removing and adding elements to the queue according to the elimination rules. We continue this process until only one person remains. Here's the code that solves the Josephus problem:

```cpp
while (q.size() > 1) {
    for (int i = 0; i < k - 1; i++) {
        int eliminated = q.front();
        q.pop();
        q.push(eliminated);
    }
    q.pop();
}
```

In the above code, we iterate `k-1` times and remove the front element from the queue and reinsert it at the rear. This simulates the elimination of every `k`-th person. Finally, we remove the remaining person from the queue.

Now, let's output the position of the last person standing:

```cpp
std::cout << "The position of the last person standing: " << q.front() << std::endl;
```

Finally, we need to close the main function. Here's the complete code:

```cpp
#include <iostream>
#include <queue>

int main() {
    int n, k;
    std::cout << "Enter the number of people (n): ";
    std::cin >> n;
    std::cout << "Enter the value of k: ";
    std::cin >> k;

    std::queue<int> q;
    for (int i = 1; i <= n; i++) {
        q.push(i);
    }

    while (q.size() > 1) {
        for (int i = 0; i < k - 1; i++) {
            int eliminated = q.front();
            q.pop();
            q.push(eliminated);
        }
        q.pop();
    }

    std::cout << "The position of the last person standing: " << q.front() << std::endl;

    return 0;
}
```

## Conclusion

In this blog post, we discussed how to solve the Josephus problem using a queue in C++. We leveraged the `std::queue` class to simulate the elimination process efficiently. By removing and reinserting elements in a queue, we were able to find the position of the last person standing.

Feel free to experiment with different values of `n` and `k` to explore different scenarios of the Josephus problem. The provided code can be a starting point for further enhancements or modifications. Happy coding!

#tags: #cpp #queue