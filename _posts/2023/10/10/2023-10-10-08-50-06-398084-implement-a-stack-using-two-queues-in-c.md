---
layout: post
title: "Implement a stack using two queues in C++"
description: " "
date: 2023-10-10
tags: [stacks, queues]
comments: true
share: true
---
A stack is a data structure that follows the Last-In-First-Out (LIFO) principle, where the last element pushed into the stack is the first one to be popped out. Although a stack can be easily implemented directly using an array or a linked list, we can also implement a stack using two queues.

## What is a Queue?
A queue is another common data structure that follows the First-In-First-Out (FIFO) principle, where the first element enqueued is the first one to be dequeued. A queue can be implemented using an array or a linked list.

## Using Two Queues to Implement a Stack
To implement a stack using two queues, we need to maintain two queues: `queue1` and `queue2`. The basic idea is to use one queue for storing elements and the other as a temporary queue to support stack operations.

Here's the implementation of a stack using two queues in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

class Stack {
private:
    queue<int> primaryQueue;
    queue<int> secondaryQueue;

public:
    void push(int val) {
        secondaryQueue.push(val);

        while (!primaryQueue.empty()) {
            secondaryQueue.push(primaryQueue.front());
            primaryQueue.pop();
        }

        swap(primaryQueue, secondaryQueue);
    }

    void pop() {
        if (!primaryQueue.empty()) {
            primaryQueue.pop();
        }
    }

    int top() {
        if (!primaryQueue.empty()) {
            return primaryQueue.front();
        }
        return -1; // return -1 if stack is empty
    }

    bool empty() {
        return primaryQueue.empty();
    }
};

int main() {
    Stack s;
    s.push(5);
    s.push(10);
    s.push(15);

    cout << "Top element: " << s.top() << endl;
    s.pop();

    cout << "Top element after pop: " << s.top() << endl;
    s.push(20);

    cout << "Is stack empty? " << (s.empty() ? "Yes" : "No") << endl;

    return 0;
}
```

## Explanation
1. Two queues (`primaryQueue` and `secondaryQueue`) are declared as private members of the `Stack` class.
   
2. The `push` operation is performed by pushing the element into the `secondaryQueue`. Then, all the elements from the `primaryQueue` are transferred to the `secondaryQueue` one by one. Finally, the `primaryQueue` and `secondaryQueue` are swapped.
   
3. The `pop` operation is simply performed by popping the front element of the `primaryQueue`.
   
4. The `top` operation returns the front element of the `primaryQueue` if it is not empty, otherwise it returns -1 to indicate an empty stack.
   
5. The `empty` operation checks if the `primaryQueue` is empty or not and returns a boolean value accordingly.

## Conclusion
In this blog post, we have covered the implementation of a stack using two queues in C++. Using this approach, we can easily implement stack operations like push, pop, top, and check if the stack is empty. This implementation provides an alternative way to implement stacks and showcases the versatility of queues in data structures.

#stacks #queues