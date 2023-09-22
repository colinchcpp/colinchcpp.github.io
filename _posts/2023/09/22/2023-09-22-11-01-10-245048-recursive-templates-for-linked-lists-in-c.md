---
layout: post
title: "Recursive templates for linked lists in C++"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

When implementing linked lists in C++, we often need to manipulate them using recursive operations. One way to achieve this is by leveraging recursive templates. In this blog post, we will explore how to use recursive templates to work with linked lists in C++.

## The LinkedList Class

Before diving into recursive templates, let's define a simple `LinkedList` class that represents a node in the linked list:

```cpp
template <typename T>
class LinkedList
{
public:
    T data;
    LinkedList<T>* next;

    LinkedList(T value)
    {
        data = value;
        next = nullptr;
    }
};
```

## Recursive Operations

### 1. Recursive Print

To print all the elements of a linked list, we can define a recursive print function:

```cpp
template <typename T>
void PrintLinkedList(const LinkedList<T>* head)
{
    if (head == nullptr)
    {
        return;
    }

    std::cout << head->data << " ";
    PrintLinkedList(head->next);
}
```

### 2. Recursive Insertion

To insert an element at the end of a linked list using recursion, we can define a recursive insertion function:

```cpp
template <typename T>
void InsertAtEnd(LinkedList<T>*& head, T value)
{
    if (head == nullptr)
    {
        head = new LinkedList<T>(value);
        return;
    }

    InsertAtEnd(head->next, value);
}
```

### 3. Recursive Searching

To check if an element exists in a linked list using recursion, we can define a recursive search function:

```cpp
template <typename T>
bool SearchElement(const LinkedList<T>* head, T value)
{
    if (head == nullptr)
    {
        return false;
    }

    if (head->data == value)
    {
        return true;
    }

    return SearchElement(head->next, value);
}
```

### 4. Recursive Deletion

To delete an element from a linked list using recursion, we can define a recursive deletion function:

```cpp
template <typename T>
void DeleteElement(LinkedList<T>*& head, T value)
{
    if (head == nullptr)
    {
        return;
    }

    if (head->data == value)
    {
        LinkedList<T>* temp = head;
        head = head->next;
        delete temp;
        return;
    }

    DeleteElement(head->next, value);
}
```

## Example Usage

Let's see how we can use the recursive template operations on a linked list:

```cpp
int main()
{
    LinkedList<int>* head = nullptr;

    // Inserting elements
    InsertAtEnd(head, 10);
    InsertAtEnd(head, 20);
    InsertAtEnd(head, 30);

    // Printing elements
    std::cout << "Linked List: ";
    PrintLinkedList(head);
    std::cout << std::endl;

    // Searching an element
    int element = 20;
    if (SearchElement(head, element))
    {
        std::cout << element << " is present in the linked list." << std::endl;
    }
    else
    {
        std::cout << element << " is not present in the linked list." << std::endl;
    }

    // Deleting an element
    DeleteElement(head, 20);

    // Printing elements after deletion
    std::cout << "Linked List after deletion: ";
    PrintLinkedList(head);
    std::cout << std::endl;

    return 0;
}
```

## Conclusion

Recursive templates provide a powerful way to manipulate linked lists in C++. By utilizing recursive operations, such as printing, insertion, searching, and deletion, we can efficiently work with linked lists. Understanding and using recursive templates can greatly simplify linked list operations in C++.