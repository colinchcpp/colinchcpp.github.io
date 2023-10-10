---
layout: post
title: "Implement a queue using two stacks in C++"
description: " "
date: 2023-10-10
tags: [TechTips, DataStructure]
comments: true
share: true
---

In this article, we will explore how to implement a Queue data structure using two Stacks in C++. A Queue follows the First-In-First-Out (FIFO) principle, which means the element that is inserted first will be the first one to be removed.

Stacks and queues are fundamental data structures in programming. While a stack follows the Last-In-First-Out (LIFO) principle, a queue follows the FIFO principle. By using two stacks cleverly, we can implement a queue efficiently.

## The Approach

To implement a queue using two stacks, we can use one stack to handle the enqueue operation and another stack to handle the dequeue operation. The idea is to transfer elements between the two stacks as needed.

The primary stack, called **StackEn**, will be used for enqueueing elements. Whenever we need to enqueue an element, we simply push it onto StackEn.

The secondary stack, called **StackDe**, will be used for dequeueing elements. When we need to dequeue an element, we check if StackDe is empty. If it's not empty, we pop the element from StackDe and return it. If it's empty, we transfer all the elements from StackEn to StackDe. By doing so, the order of elements is reversed, effectively simulating the behavior of a queue.

Let's see how this can be implemented in C++.

## Implementation

```cpp
#include <iostream>
#include <stack>

class Queue {
private:
    std::stack<int> stackEn;
    std::stack<int> stackDe;

public:
    void enqueue(int value) {
        stackEn.push(value);
    }

    int dequeue() {
        if (stackDe.empty()) {
            while (!stackEn.empty()) {
                int value = stackEn.top();
                stackEn.pop();
                stackDe.push(value);
            }
        }

        int value = stackDe.top();
        stackDe.pop();
        return value;
    }

    bool isEmpty() {
        return stackEn.empty() && stackDe.empty();
    }
};
```

In the above code, we define a **Queue** class that contains two private stacks: **stackEn** for enqueueing elements and **stackDe** for dequeueing elements. The class has three member functions:

- **enqueue()**: This function simply pushes the given element onto the StackEn.

- **dequeue()**: This function checks if StackDe is empty. If it is, it transfers all the elements from StackEn to StackDe. It then pops the top element from StackDe and returns it.

- **isEmpty()**: This function checks if both StackEn and StackDe are empty, indicating that the queue is empty.

## Usage

Let's see an example of how to use the implemented queue.

```cpp
int main() {
    Queue queue;

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    std::cout << queue.dequeue() << std::endl; // Output: 10
    std::cout << queue.dequeue() << std::endl; // Output: 20

    queue.enqueue(40);

    std::cout << queue.dequeue() << std::endl; // Output: 30
    std::cout << queue.dequeue() << std::endl; // Output: 40

    std::cout << queue.isEmpty() << std::endl; // Output: 1 (true)

    return 0;
}
```

In the above code, we create an instance of the **Queue** class and perform enqueue and dequeue operations. We also check if the queue is empty using the **isEmpty()** function.

## Conclusion

In this article, we learned how to implement a queue using two stacks in C++. By leveraging the properties of stacks, we efficiently achieved the FIFO behavior of a queue. This implementation can be useful in various scenarios where we need to maintain the order of elements while performing enqueue and dequeue operations.

Try implementing the queue using two stacks yourself and experiment with different scenarios. Happy coding!

#TechTips #DataStructure