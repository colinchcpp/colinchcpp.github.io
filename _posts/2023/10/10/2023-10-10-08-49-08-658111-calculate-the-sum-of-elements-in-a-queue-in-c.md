---
layout: post
title: "Calculate the sum of elements in a queue in C++"
description: " "
date: 2023-10-10
tags: [programming]
comments: true
share: true
---

In this blog post, we will discuss how to calculate the sum of all elements in a queue using C++. A queue is a data structure that follows the First-In-First-Out (FIFO) principle, where elements are inserted at the rear and removed from the front. We will use the standard template library (STL) provided by C++ to implement this functionality.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Implementation](#implementation)
- [Example Usage](#example-usage)
- [Conclusion](#conclusion)

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of C++ and its syntax. It is also recommended to have an IDE or text editor to write and compile your code.

## Implementation

Let's begin by creating a `sumQueue` function that takes a queue of integers as a parameter and returns the sum of all its elements. 

```cpp
#include <iostream>
#include <queue>

int sumQueue(std::queue<int> q) {
    int sum = 0;
    while (!q.empty()) {
        sum += q.front();
        q.pop();
    }
    return sum;
}
```

We declare an `int` variable `sum` to store the sum of elements and initialize it to 0. We then iterate over the queue using a `while` loop until the queue becomes empty. Inside the loop, we add the front element of the queue to `sum` and remove it using the `pop` function. Finally, we return the sum.

## Example Usage

Now, let's see an example of how to use the `sumQueue` function with a sample queue of integers.

```cpp
int main() {
    std::queue<int> myQueue;
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);
    myQueue.push(50);
    
    int queueSum = sumQueue(myQueue);
    
    std::cout << "Sum of elements in the queue: " << queueSum << std::endl;
    
    return 0;
}
```

In this example, we create a queue called `myQueue` and push five integers into it. Then, we call the `sumQueue` function passing `myQueue` as an argument and store the returned sum in the `queueSum` variable. Finally, we output the sum of the elements in the queue using `std::cout`.

## Conclusion

In this blog post, we have learned how to calculate the sum of elements in a queue using C++. By iterating over the queue and adding the elements to a variable, we can easily compute the total sum. This functionality can be useful in various scenarios such as analyzing data or solving mathematical problems. Explore different applications and experiment with queues to further enhance your C++ programming skills.

#programming #C++