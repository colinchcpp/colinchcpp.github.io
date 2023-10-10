---
layout: post
title: "Queue data structure vs. linked list in C++"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

When implementing data structures in C++, two commonly used options are queues and linked lists. Both offer different capabilities and are suitable for different scenarios. In this blog post, we will compare the queue data structure with the linked list to help you understand their differences and choose the appropriate one for your needs.

## Queue Data Structure

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. It allows elements to be inserted at the back and removed from the front. Think of it as standing in a line, where the person who arrives first gets served first.

In C++, queues are typically implemented using the `std::queue` container from the Standard Template Library (STL). This container provides a simple and efficient way to handle queue operations like enqueue (push) and dequeue (pop).

Here's an example of how to use `std::queue` in C++:

```cpp
#include <queue>

int main() {
   std::queue<int> myQueue;

   myQueue.push(5);        // Insert element 5 at the back of the queue
   myQueue.push(10);       // Insert element 10 at the back of the queue
   myQueue.push(15);       // Insert element 15 at the back of the queue

   int frontElement = myQueue.front();    // Get the front element (5)
   myQueue.pop();                         // Remove the front element (5)

   int queueSize = myQueue.size();        // Get the size of the queue (2)

   return 0;
}
```

## Linked List

A linked list is a data structure where elements are connected using pointers. Each element (node) in the list contains data and a pointer to the next node in the sequence. Unlike an array or a vector, linked lists allow dynamic memory allocation, which means elements can be easily inserted or removed at any position.

In C++, you can create a linked list by implementing your own class or by using existing libraries like the `std::list` container from the STL.

Here's an example of how to use `std::list` in C++:

```cpp
#include <list>

int main() {
   std::list<int> myList;

   myList.push_back(5);     // Insert element 5 at the back of the list
   myList.push_back(10);    // Insert element 10 at the back of the list
   myList.push_back(15);    // Insert element 15 at the back of the list

   int frontElement = myList.front();    // Get the front element (5)
   myList.pop_front();                    // Remove the front element (5)

   int listSize = myList.size();         // Get the size of the list (2)

   return 0;
}
```

## Comparing Queue and Linked List

Now that we have seen how to use queues and linked lists in C++, let's compare them based on some common aspects:

1. **Insertion and deletion:** Queues are optimized for efficient insertion and deletion at the front and back. Linked lists, on the other hand, allow insertion and deletion at any position.

2. **Access time:** Both queues and linked lists provide fast access to the front element. However, accessing an element at a specific position in a linked list requires traversing the list from the beginning.

3. **Memory allocation:** Linked lists dynamically allocate memory for each node, allowing flexibility in memory usage compared to fixed-size arrays. Queues, in most cases, are implemented using linked lists or arrays internally.

4. **Size limitations:** Linked lists can grow dynamically to accommodate elements, while queues may have size restrictions based on the underlying implementation.

Based on these comparisons, if you need a data structure that follows the FIFO principle and provides efficient insertion and deletion at the front and back, a queue data structure is a suitable choice. On the other hand, if you require flexible insertion and deletion at any position, a linked list is a better option.

In conclusion, understanding the differences between queues and linked lists in C++ will help you make informed decisions when selecting the appropriate data structure for your specific needs.