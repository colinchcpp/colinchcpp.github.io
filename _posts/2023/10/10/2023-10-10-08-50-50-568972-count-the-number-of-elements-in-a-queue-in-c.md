---
layout: post
title: "Count the number of elements in a queue in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

In this blog post, we will discuss how to count the number of elements in a queue in C++. 

A queue is a data structure that follows the **FIFO** (First-In, First-Out) principle. It stores elements and allows two basic operations - enqueue (add element to the back of the queue) and dequeue (remove element from the front of the queue). 

To count the number of elements in a queue, you can use the `size()` method provided by the Standard Template Library (STL) in C++. 

Here's an example code snippet that demonstrates this:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a queue
    std::queue<int> myQueue;

    // Enqueue elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);

    // Get the number of elements in the queue
    int count = myQueue.size();

    std::cout << "Number of elements in the queue: " << count << std::endl;

    return 0;
}
```

In the above code, we first create a queue called `myQueue` using the `std::queue<int>` syntax. We then enqueue four elements using the `push()` method.

To get the number of elements in the queue, we use the `size()` method and store the result in the `count` variable. Finally, we print the count using `std::cout`.

When you run this code, the output will be:

```
Number of elements in the queue: 4
```

By using the `size()` method provided by the STL, you can easily count the number of elements in a queue in C++. This is a simple and efficient way to track the size of your queue and perform operations accordingly.

I hope you found this blog post helpful! Stay tuned for more C++ programming tips and tricks. #C++ #Queue