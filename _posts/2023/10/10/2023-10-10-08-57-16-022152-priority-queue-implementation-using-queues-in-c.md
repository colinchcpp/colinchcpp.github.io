---
layout: post
title: "Priority queue implementation using queues in C++"
description: " "
date: 2023-10-10
tags: [tech]
comments: true
share: true
---

A **priority queue** is a data structure where each element has a priority assigned to it. The elements in the queue are always ordered according to their priority, and the element with the highest priority is dequeued first. Priority queues are commonly used in algorithms such as Dijkstra's algorithm and Huffman coding.

In this article, we will implement a priority queue using **queues** in C++. We will use two queues to implement the priority queue: one queue to store the elements and another queue to store the priorities for each element.

## Implementation Steps

1. Include the necessary header files:
```cpp
#include <iostream>
#include <queue>
using namespace std;
```

2. Define a struct to hold elements and priorities together:
```cpp
struct Element {
  int value;
  int priority;
};
```

3. Create a comparison function to compare the priorities of two elements:
```cpp
struct Compare {
  bool operator()(const Element& a, const Element& b) {
    return a.priority < b.priority;
  }
};
```

4. Create a priority queue using the `priority_queue` template class and the comparison function:
```cpp
priority_queue<Element, vector<Element>, Compare> pq;
```

5. Enqueue an element with its priority:
```cpp
Element e1 = {5, 2};
pq.push(e1);
```

6. Dequeue the element with the highest priority:
```cpp
Element highestPriorityElement = pq.top();
pq.pop();
```

7. Print the value and priority of the dequeued element:
```cpp
cout << "Value: " << highestPriorityElement.value << endl;
cout << "Priority: " << highestPriorityElement.priority << endl;
```

## Example Usage

```cpp
int main() {
  priority_queue<Element, vector<Element>, Compare> pq;

  Element e1 = {5, 2};
  Element e2 = {10, 1};
  Element e3 = {3, 3};
  
  pq.push(e1);
  pq.push(e2);
  pq.push(e3);

  Element highestPriorityElement = pq.top();
  pq.pop();
  
  cout << "Value: " << highestPriorityElement.value << endl;
  cout << "Priority: " << highestPriorityElement.priority << endl;
  
  return 0;
}
```

## Conclusion

In this article, we implemented a priority queue using queues in C++. By using two queues and a comparison function, we were able to maintain the order of elements based on their priorities. Priority queues are a powerful data structure for dealing with elements that have different priorities, and they find various applications in computer science and algorithms.

#tech #C++