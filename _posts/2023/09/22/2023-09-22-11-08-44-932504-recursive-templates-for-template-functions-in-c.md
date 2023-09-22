---
layout: post
title: "Recursive templates for template functions in C++"
description: " "
date: 2023-09-22
tags: [Templates]
comments: true
share: true
---

In C++, templates provide a powerful mechanism to write generic code. They allow us to write functions or classes that can operate on different types without sacrificing type safety. Recursive templates further extend this functionality by enabling us to work with complex data structures.

Recursive templates refer to the technique of defining a template function that calls itself as part of its computation. This approach is particularly useful when working with recursive data structures such as linked lists, trees, or nested containers.

## Template Function for Finding the Sum of Elements in a Linked List

Let's consider an example of finding the sum of elements in a linked list using a recursive template function in C++.

```cpp
#include <iostream>

template<typename T>
struct Node
{
    T data;
    Node<T>* next;
};

template<typename T>
T sumLinkedList(const Node<T>* head)
{
    if (head == nullptr) {
        return 0;
    }
    return head->data + sumLinkedList(head->next);
}

int main()
{
    Node<int> node1{1, nullptr};
    Node<int> node2{2, nullptr};
    Node<int> node3{3, nullptr};
    node1.next = &node2;
    node2.next = &node3;

    int sum = sumLinkedList(&node1);
    std::cout << "Sum of elements in the linked list: " << sum << std::endl;

    return 0;
}
```

In the above code, we define a `Node` struct that represents a node in a linked list. We then define a recursive template function called `sumLinkedList` which takes a pointer to the head of the linked list as input and returns the sum of all elements in the list.

The `sumLinkedList` function checks if the current node is `nullptr`, indicating the end of the list. If it is, the function returns 0. Otherwise, it adds the data of the current node to the sum of the remaining list obtained by calling `sumLinkedList` recursively with the next node.

In the main function, we create a linked list with three nodes and call `sumLinkedList` with the head node to calculate the sum. The result is then printed to the console.

## Conclusion

Recursive templates in C++ allow us to write flexible, generic code that can handle recursive data structures efficiently. By leveraging the power of templates, we can write algorithms that work seamlessly with various types, promoting code reusability and maintainability.

#C++ #Templates