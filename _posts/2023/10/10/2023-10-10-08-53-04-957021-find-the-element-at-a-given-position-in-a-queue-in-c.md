---
layout: post
title: "Find the element at a given position in a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

Queues are a fundamental data structure in computer science that follow the **FIFO (First-In-First-Out)** principle. In C++, the Standard Template Library (STL) provides the `queue` container that allows you to efficiently implement queues.

In this article, we will discuss how to find the element at a specific position in a `queue` in C++. Let's dive in!

## 1. Create and populate the queue

First, we need to create a queue and add elements to it. Here's an example:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    // Pushing elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);
    myQueue.push(50);

    return 0;
}
```

In the above code, we created a `queue` called `myQueue` and added some integers to it using the `push` method.

## 2. Find the element at a given position

To find the element at a specific position in the queue, we have to iterate through the elements until we reach the desired position. Unfortunately, the `queue` container in C++ does not provide direct indexing like an array or vector.

Here's an example function that finds the element at a given position in a queue:

```cpp
int getElementAt(const std::queue<int>& myQueue, int position) {
    std::queue<int> tempQueue = myQueue;

    while (position > 0 && !tempQueue.empty()) {
        tempQueue.pop();
        position--;
    }

    if (position == 0 && !tempQueue.empty()) {
        return tempQueue.front();
    }

    throw std::out_of_range("Invalid position");
}
```

In the above code, the `getElementAt` function takes a `queue`, `myQueue`, and a `position` as parameters. It creates a temporary queue, `tempQueue`, and iterates through the elements until the desired position is reached. If the position is valid, it returns the value of the front element. Otherwise, it throws an `std::out_of_range` exception.

## 3. Usage example

Let's use the `getElementAt` function to find the element at a specific position in our `myQueue`:

```cpp
int main() {
    std::queue<int> myQueue;
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);
    myQueue.push(50);

    int position = 2;
    try {
        int element = getElementAt(myQueue, position);
        std::cout << "Element at position " << position << ": " << element << std::endl;
    } catch (const std::out_of_range& e) {
        std::cerr << "Invalid position: " << e.what() << std::endl;
    }

    return 0;
}
```

In the above code, we find the element at position 2 in the `myQueue` queue. If the position is valid, it prints the element value; otherwise, it displays an error message.

## Conclusion

Although the `queue` container in C++ does not provide direct indexing, we can still find the element at a specific position by iterating through the elements. By following the steps outlined in this article, you can easily find elements based on their positions in a queue.

I hope you found this article helpful. Happy coding!

--------------
##### Tags: C++, queue, data structure