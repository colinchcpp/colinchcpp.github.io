---
layout: post
title: "Implementation of queues using templates in C++"
description: " "
date: 2023-10-10
tags: [programming, templates]
comments: true
share: true
---

When working with data structures in C++, templates allow us to create reusable code that can work with multiple data types. In this blog post, we will explore how to implement a queue data structure using templates in C++.

## What is a Queue?

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. In a queue, elements are added to the back and removed from the front of the queue. This is similar to a queue of people waiting in line, where the person who has been waiting the longest is served first.

## Implementing a Queue using Templates

To implement a queue using templates in C++, we will use a linked list as the underlying data structure. The linked list will hold the elements of the queue, and we can add or remove elements by modifying the head and tail pointers.

Let's start by defining a `Queue` class template, which will have two private member variables - `head` and `tail` pointers to keep track of the front and back of the queue, respectively.

```cpp
template<typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
    };
    Node* head;
    Node* tail;
public:
    // Constructor
    Queue() : head(nullptr), tail(nullptr) {}
    
    // Destructor to deallocate memory
    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    // Check if the queue is empty
    bool isEmpty() {
        return head == nullptr;
    }
    
    // Enqueue an element to the back of the queue
    void enqueue(const T& element) {
        Node* newNode = new Node;
        newNode->data = element;
        newNode->next = nullptr;
        
        if (isEmpty()) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }
    
    // Dequeue an element from the front of the queue
    void dequeue() {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        
        Node* temp = head;
        head = head->next;
        
        delete temp;
    }
    
    // Get the front element of the queue
    T front() {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty");
        }
        
        return head->data;
    }
};
```

In the above code, we have defined a `Node` struct to represent each element in the queue. We then declare the `head` and `tail` pointers, which initially point to `nullptr`. The constructor initializes the queue as empty. The `isEmpty()` function checks if the queue is empty or not.

The `enqueue()` function adds an element to the back of the queue. If the queue is empty, the `head` and `tail` pointers are set to the new node. Otherwise, the `next` pointer of the `tail` node is set to the new node, and the `tail` pointer is updated.

The `dequeue()` function removes the element from the front of the queue. If the queue is empty, an exception is thrown. The `head` pointer is updated to point to the next node, and the memory of the removed node is deallocated.

The `front()` function returns the front element of the queue. If the queue is empty, an exception is thrown.

## Using the Queue

Now that we have implemented the queue using templates, we can use it to create a queue of any data type. Here's an example of how we can use the `Queue` class template:

```cpp
int main() {
    Queue<int> intQueue;
    intQueue.enqueue(5);
    intQueue.enqueue(10);
    intQueue.enqueue(15);
    
    std::cout << "Front element: " << intQueue.front() << std::endl;
    
    intQueue.dequeue();
    
    std::cout << "Front element after dequeue: " << intQueue.front() << std::endl;
    
    return 0;
}
```

In the above code, we create an instance of `Queue` class template for `int` data type. We enqueue three integer values and then print the front element. After dequeueing an element, we print the front element again.

## Conclusion

In this blog post, we have explored how to implement queues using templates in C++. The use of templates allows us to create a generic queue data structure that can be used with different data types. This provides flexibility and reusability in our code. By using a linked list as the underlying data structure, we can efficiently implement the First-In-First-Out principle of a queue.

Implementing queues using templates can be incredibly useful in various scenarios, such as implementing task queues, message queues, and more. Use this implementation as a foundation to handle queues in your C++ projects efficiently.

#programming #templates